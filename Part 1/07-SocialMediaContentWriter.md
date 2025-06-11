## Social Media Content Writer



```python
# !pip install crewai
# !pip install crewai-tools
# !pip  install firecrawl-py
```


```python
from dotenv import load_dotenv
load_dotenv()

from crewai import Agent, Task, Crew
from crewai.flow.flow import Flow, start, listen

import openai
import os

openai_client = openai.OpenAI(api_key = os.getenv("OPENAI_API_KEY"))
```


```python
import yaml

with open('notebook6/config/planner_agents.yaml', 'r') as f:
    agents_config = yaml.safe_load(f)

with open('notebook6/config/planner_tasks.yaml', 'r') as f:
    tasks_config = yaml.safe_load(f)
```


```python
from pydantic import BaseModel
from typing import Optional

class Tweet(BaseModel):
    """Represents an individual tweet in a thread"""
    content: str
    is_hook: bool = False 
    media_urls: Optional[list[str]] = []

class Thread(BaseModel):
    """Represents a Twitter thread"""
    topic: str 
    tweets: list[Tweet]

class LinkedInPost(BaseModel):
    """Represents a LinkedIn post"""
    content: str  # The main content of the post
    media_url: str # Main image URL for the post
```


```python
from crewai_tools import DirectoryReadTool, FileReadTool 

all_tools = [DirectoryReadTool(), FileReadTool()]
```

    /Users/g/miniconda3/envs/agents/lib/python3.11/site-packages/pydantic/_internal/_generate_schema.py:623: UserWarning: <built-in function callable> is not a Python type (it may be an instance of an object), Pydantic will allow any object with no validation since we cannot even enforce that the input is an instance of the given type. To get rid of this error wrap the type with `pydantic.SkipValidation`.
      warn(



```python
from crewai import Agent, Task

draft_analyzer = Agent(config=agents_config['draft_analyzer'],
                       tools=all_tools,
                       llm = "gpt-3.5-turbo")

analyze_draft = Task(config=tasks_config['analyze_draft'],
                     agent=draft_analyzer
                     )



twitter_thread_planner = Agent(config=agents_config['twitter_thread_planner'],
                               tools=all_tools,
                               llm = "gpt-3.5-turbo")

create_twitter_thread_plan = Task(config=tasks_config['create_twitter_thread_plan'],
                                  agent=twitter_thread_planner,
                                  output_pydantic=Thread)



linkedin_post_planner = Agent(config=agents_config['linkedin_post_planner'],
                              tools=all_tools,
                              llm = "gpt-3.5-turbo")

create_linkedin_post_plan = Task(config=tasks_config['create_linkedin_post_plan'],
                                 agent=linkedin_post_planner,
                                 output_pydantic=LinkedInPost)
```


```python
twitter_planning_crew = Crew(
    agents=[draft_analyzer, twitter_thread_planner],
    tasks=[analyze_draft, create_twitter_thread_plan],
    verbose=True
)

linkedin_planning_crew = Crew (
    agents=[draft_analyzer, linkedin_post_planner],
    tasks=[analyze_draft, create_linkedin_post_plan],
    verbose=True
)
```


```python
from pydantic import BaseModel
from pathlib import Path

class ContentPlanningState(BaseModel):
    """
    State for the content planning flow
    """
    # URL of the blog to scrape
    blog_post_url: str = "https://www.dailydoseofds.com/ai-agents-crash-course-part-4-with-implementation/#demo-1-social-media-content-writer-flow"
    
    # Path where the scraped content will be stored
    draft_path: Path = "assets/"
    
    # Determines whether to create a Twitter or LinkedIn post 
    post_type: str = "twitter"  
    
    # Example Twitter threads for style reference
    path_to_example_threads: str = "assets/example_threads.txt" 
    
    # Example LinkedIn posts for reference
    path_to_example_linkedin: str = "assets/example_linkedin.txt"



from firecrawl import FirecrawlApp
import os
import json
import uuid
from crewai.flow.flow import Flow, start, listen, router, or_

class CreateContentPlanningFlow(Flow[ContentPlanningState]):

    @start()
    def scrape_blog_post(self):
        print(f"# Fetching draft from: {self.state.blog_post_url}")

        # Initialize FireCrawl
        app = FirecrawlApp(api_key=os.getenv("FIRECRAWL_API_KEY"))
        
        # Scrape the blog post in Markdown and HTML format
        scrape_result = app.scrape_url(self.state.blog_post_url,
                                       params={'formats': ['markdown', 'html']})

        # Extract the title (fallback to a UUID if not found)
        try:
            title = scrape_result['metadata']['title']
        except Exception:
            title = str(uuid.uuid4())

        # Store the scraped content as a markdown file
        self.state.draft_path = f'assets/{title}.md'
        with open(self.state.draft_path, 'w') as f:
            f.write(scrape_result['markdown'])

        return self.state
    
    @router(scrape_blog_post)
    def select_platform(self):
        if self.state.post_type == "twitter":
            return "twitter"
        elif self.state.post_type == "linkedin":
            return "linkedin"
        

    @listen("twitter")
    def twitter_draft(self):
        print(f"# Planning content for: {self.state.draft_path}")
    
        # Execute the Twitter Planning Crew
        result = twitter_planning_crew.kickoff(inputs={
            'draft_path': self.state.draft_path, 
            'path_to_example_threads': self.state.path_to_example_threads
        })
    
        print(f"# Planned content for {self.state.draft_path}:")
    
        # Print each tweet in the generated thread
        for i, tweet in enumerate(result.pydantic.tweets):
            print(f"Tweet {i+1}: {tweet.content}")
            print(f"Media URLs: {tweet.media_urls}")
            print("-" * 100)
    
        return result

    @listen("linkedin")
    def linkedin_draft(self):
        print(f"# Planning content for: {self.state.draft_path}")
    
        # Execute the LinkedIn Planning Crew
        result = linkedin_planning_crew.kickoff(inputs={
            'draft_path': self.state.draft_path, 
            'path_to_example_linkedin': self.state.path_to_example_linkedin
        })
    
        print(f"# Planned content for {self.state.draft_path}:")
        print(f"{result.pydantic.content}")
    
        return result
    
    @listen(or_(twitter_draft, linkedin_draft))
    def save_plan(self, plan):
        with open(f'output/draft.json', 'w') as f:
            json.dump(plan.pydantic.model_dump(), f, indent=2)
```


```python
flow = CreateContentPlanningFlow()
```


```python
flow.kickoff()
```


```python
flow.plot()
```
