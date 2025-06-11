# Human In Loop


Below, let’s build a human-in-the-loop AI research system, where:

- An AI Researcher gathers and summarizes key industry insights.\
- A human reviewer checks and validates the AI-generated research.
- An AI Content Strategist writes a blog post based on the reviewed research.
- A human reviewer ensures the content is well-structured before publishing.


```python
from crewai import Agent, LLM

llm = LLM(model="gpt-4o")

researcher_agent = Agent(
    role="Senior AI Researcher",
    goal="""Discover and summarize the latest
            trends in AI and technology.""",
    backstory="""An expert in AI research who tracks
                 emerging trends and their real-world applications.""",
    verbose=True,
    allow_delegation=False,
    llm=llm
)

content_strategist_agent = Agent(
    role="Tech Content Strategist",
    goal="""Transform AI research insights
            into compelling blog content.""",
    backstory="""An experienced tech writer who makes
                 AI advancements accessible to a broad audience.""",
    verbose=True,
    allow_delegation=True,
    llm=llm
)


from crewai import Task

ai_research_task = Task(
    description=(
            "Conduct a deep analysis of AI trends in 2025. "
            "Identify key innovations, breakthroughs, and market shifts. "
            "Before finalizing, ask a human reviewer "
            "for feedback to refine the report."
    ),
    expected_output="""A structured research summary
                       covering AI advancements in 2025.""",
    agent=researcher_agent,
    human_input=True   #Human In Loop
)

blog_post_task = Task(
    description=(
        "Using insights from the AI Researcher, create an "
        " engaging blog post summarizing key AI advancements. "
        "Ensure the post is informative and accessible. Before "
        "finalizing, ask a human reviewer for approval."
    ),
    expected_output="A well-structured blog post on AI trends in 2025.",
    agent=content_strategist_agent,
    human_input=True   #Human In Loop
)
```


```python

```
