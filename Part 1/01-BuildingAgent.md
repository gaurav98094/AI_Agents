### Setup


```python
# !pip install crewai
# !pip install crewai-tools
```


```python
# ollama pull llama3.2:1b
```

### Imports


```python
from crewai import Agent, Task, Crew

from dotenv import load_dotenv
load_dotenv()
```




    True



### Define Agents

In CrewAi, Agents has
- role : expertise of system.
- goal : objective of agent
- backstory : context on personality of agent.
- tools : tools agent can use while performing tasks.


```python
senior_technical_writer = Agent(
    role = "Senior Technical Writer",
    goal = """Craft clear engagine, and well-structured
            technical content based on research findings""",
    backstory = """You are an experienced technical writer
            with expertise in simplifying complex
            concepts, structuring content for readability,
            and ensuring accuracy in documentation""",
    verbose = True,
    llm = "gpt-3.5-turbo"
)
```


```python
research_analyst = Agent(
    role = "Senior Research Analyst",
    goal = """Find, analyze, and summarize information 
            from various sources to support technical 
            and business-related inquiries.""",
    backstory = """You are a skilled research analyst with expertise 
                 in gathering accurate data, identifying key trends, 
                 and presenting insights in a structured manner.""",
    llm = "gpt-3.5-turbo",
    verbose = True
)
```


```python
code_reviewer = Agent(
    role = "Senior Code Reviewer",
    goal = """Review code for bugs, inefficiencies, and 
            security vulnerabilities while ensuring adherence 
            to best coding practices.""",
    backstory = """You are a seasoned software engineer with years of 
                 experience in writing, reviewing, and optimizing 
                 production-level code in multiple programming languages.""",
    llm = "gpt-3.5-turbo",
    verbose = True
)
```


```python
legal_reviewer = Agent(
    role = "Legal Document Expert Reviewer",
    goal = """Review contracts and legal documents to 
            ensure compliance with applicable laws and 
            highlight potential risks.""",
    backstory = """You are a legal expert with deep knowledge 
                 of contract law, regulatory frameworks, 
                 and risk mitigation strategies.""",
    llm = "gpt-3.5-turbo",
    verbose = True
)
```

### Define Tasks
A task consiste of:
- description : you can define parameter here
- agent
- expected_output


```python
writing_task = Task(
    description = """Write a well-structured, engaging,
                   and technically accurate article
                   on {topic}.""",
    agent = senior_technical_writer,     
    expected_output = """A polished, detailed, and easy-to-read
                       article on the given topic.""",
)
```

### Define Crew
A crew consists of
- agents : list of all agents that will work together in a crew.
- tasks : list of all tasks thats needed to be completed.


```python
crew = Crew(
    agents = [senior_technical_writer],
    tasks = [writing_task],
    verbose = True
)
```


```python
response = crew.kickoff(
    inputs = {
        "topic" : "Impact of AI on Data Scientist Roles in 100 words"
    }
)
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080">╭──────────────────────────────────────────── Crew Execution Started ─────────────────────────────────────────────╮</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>                                                                                                                 <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>  <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">Crew Execution Started</span>                                                                                         <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008080; text-decoration-color: #008080">crew</span>                                                                                                     <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008080; text-decoration-color: #008080">06ad109f-41b8-46a5-aa73-90208da14b14</span>                                                                       <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>                                                                                                                 <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>                                                                                                                 <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: 0ba9880c-3283-439f-967f-bf5738539256</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: 0ba9880c-3283-439f-967f-bf5738539256</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Senior Technical Writer</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[95m# Agent:[00m [1m[92mSenior Technical Writer[00m
    [95m## Task:[00m [92mWrite a well-structured, engaging,
                       and technically accurate article
                       on Impact of AI on Data Scientist Roles in 100 words.[00m
    
    
    [1m[95m# Agent:[00m [1m[92mSenior Technical Writer[00m
    [95m## Final Answer:[00m [92m
    As artificial intelligence (AI) continues to revolutionize industries, its impact on data scientist roles is profound. Data scientists now find themselves leveraging AI tools and algorithms to analyze vast datasets with greater speed and accuracy. This shift has redefined the traditional responsibilities of data scientists, emphasizing the need for expertise in machine learning and AI model creation. Additionally, AI has automated certain data analysis tasks, allowing data scientists to focus on more complex problem-solving and strategy development. Adapting to this evolving landscape, data scientists are enhancing their skills to stay relevant and maximize the potential of AI in driving insights and innovation.[00m
    
    



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: 0ba9880c-3283-439f-967f-bf5738539256</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Senior Technical Writer</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 0ba9880c-3283-439f-967f-bf5738539256</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Senior Technical Writer</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Senior Technical Writer</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Task Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Task Completed</span>                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">0ba9880c-3283-439f-967f-bf5738539256</span>                                                                     <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Agent: </span><span style="color: #008000; text-decoration-color: #008000">Senior Technical Writer</span>                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Crew Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Crew Execution Completed</span>                                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">crew</span>                                                                                                     <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008000; text-decoration-color: #008000">06ad109f-41b8-46a5-aa73-90208da14b14</span>                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




```python
from IPython.display import Markdown
Markdown(response.raw)
```




As artificial intelligence (AI) continues to revolutionize industries, its impact on data scientist roles is profound. Data scientists now find themselves leveraging AI tools and algorithms to analyze vast datasets with greater speed and accuracy. This shift has redefined the traditional responsibilities of data scientists, emphasizing the need for expertise in machine learning and AI model creation. Additionally, AI has automated certain data analysis tasks, allowing data scientists to focus on more complex problem-solving and strategy development. Adapting to this evolving landscape, data scientists are enhancing their skills to stay relevant and maximize the potential of AI in driving insights and innovation.



## Mulit Agent System


```python
from crewai_tools import SerperDevTool

serper_dev_tool = SerperDevTool()
```


```python
research_agent = Agent(
    role = "Internet Researcher",
    goal = "Find the most relevant and recent information about a given topic.",
    backstory = """You are a skilled researcher, adept at navigating the internet 
                 and gathering high-quality, reliable information.""",
    tools = [serper_dev_tool],
    verbose = True
)

research_task = Task(
    description = """Use the SerperDevTool to search for the 
                most relevant and recent data about {topic}.
                Extract the key insights from multiple sources.""",
    agent = research_agent,
    tools = [serper_dev_tool],
    expected_output = "A detailed research report with key insights and source references."
)
```


```python
summarizer_agent = Agent(
    role = "Content Summarizer",
    goal = "Condense the key insights from research into a short and informative summary.",
    backstory = """You are an expert in distilling complex information into concise, 
                 easy-to-read summaries.""",
    verbose = True
)

summarization_task = Task(
    description = "Summarize the research report into a concise and informative paragraph. "
                "Ensure clarity, coherence, and completeness.",
    agent = summarizer_agent,
    expected_output = "A well-structured summary with the most important insights."
)
```


```python
fact_checker_agent = Agent(
    role = "Fact-Checking Specialist",
    goal = "Verify the accuracy of information and remove any misleading or false claims.",
    backstory = """You are an investigative journalist with a knack for validating facts, 
                 ensuring that only accurate information is published.""",
    tools = [serper_dev_tool],
    verbose = True
)

fact_checking_task = Task(
    description = "Verify the summarized information for accuracy using the SerperDevTool. "
                "Cross-check facts with reliable sources and correct any errors.",
    agent = fact_checker_agent,
    tools = [serper_dev_tool],
    expected_output = "A fact-checked, verified summary of the research topic."
)
```


```python
from crewai import Crew, Process

research_crew = Crew(
    agents = [research_agent, summarizer_agent, fact_checker_agent],
    tasks = [research_task, summarization_task, fact_checking_task],
    process = Process.sequential,
    verbose = True
)

result = research_crew.kickoff(
    inputs = {
        "topic": "The impact of AI on job markets"
    }
)
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080">╭──────────────────────────────────────────── Crew Execution Started ─────────────────────────────────────────────╮</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>                                                                                                                 <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>  <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">Crew Execution Started</span>                                                                                         <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008080; text-decoration-color: #008080">crew</span>                                                                                                     <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008080; text-decoration-color: #008080">68ea02fd-d221-4e0c-bbe7-217b4b169e5a</span>                                                                       <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>                                                                                                                 <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>                                                                                                                 <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[95m# Agent:[00m [1m[92mInternet Researcher[00m
    [95m## Task:[00m [92mUse the SerperDevTool to search for the 
                    most relevant and recent data about The impact of AI on job markets.
                    Extract the key insights from multiple sources.[00m



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
└── <span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🧠 </span><span style="color: #000080; text-decoration-color: #000080">Thinking...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    
    
    [1m[95m# Agent:[00m [1m[92mInternet Researcher[00m
    [95m## Thought:[00m [92mI need to gather detailed and relevant information about the impact of AI on job markets from multiple sources. I will perform a search using the specified tool to obtain recent data and insights.[00m
    [95m## Using tool:[00m [92mSearch the internet with Serper[00m
    [95m## Tool Input:[00m [92m
    "{\"search_query\": \"The impact of AI on job markets 2023\"}"[00m
    [95m## Tool Output:[00m [92m
    {'searchParameters': {'q': 'The impact of AI on job markets 2023', 'type': 'search', 'num': 10, 'engine': 'google'}, 'organic': [{'title': '[PDF] Artificial Intelligence Impact on Labor Markets', 'link': 'https://www.iedconline.org/clientuploads/EDRP%20Logos/AI_Impact_on_Labor_Markets.pdf', 'snippet': 'Artificial Intelligence (AI) has emerged as a transformative force in the labor market, reshaping the nature of work, job roles, and employment ...', 'position': 1}, {'title': 'Research: How Gen AI Is Already Impacting the Labor Market', 'link': 'https://hbr.org/2024/11/research-how-gen-ai-is-already-impacting-the-labor-market', 'snippet': 'As shown in our study, automation-prone jobs like writing and coding saw significant declines in demand while new types of work requiring AI- ...', 'position': 2}, {'title': 'How Artificial Intelligence Is Transforming The Job Market - Forbes', 'link': 'https://www.forbes.com/councils/forbestechcouncil/2025/01/10/how-artificial-intelligence-is-transforming-the-job-market-a-guide-to-adaptation-and-career-transformation/', 'snippet': 'As some positions face reductions, many new opportunities emerge, creating a net gain in employment. Moreover, as knowledge about AI grows, it ...', 'position': 3}, {'title': 'Is AI already shaking up labor market? - Harvard Gazette', 'link': 'https://news.harvard.edu/gazette/story/2025/02/is-ai-already-shaking-up-labor-market-a-i-artificial-intelligence/', 'snippet': 'Between 2013 and 2023, the share of retail sales jobs dropped from 7.5 to 5.7 percent of the job market, a reduction of 25 percent. The co- ...', 'position': 4}, {'title': 'The Impact of AI on the Future Job Market - EXIN', 'link': 'https://www.exin.com/article/the-impact-of-ai-on-the-future-job-market-understanding-the-changes/', 'snippet': 'The “Future of Jobs Report 2023” predicts that by 2027, 83 million jobs may be displaced by AI and automation, while 69 million new jobs will be created. This ...', 'position': 5}, {'title': 'Incorporating AI impacts in BLS employment projections', 'link': 'https://www.bls.gov/opub/mlr/2025/article/incorporating-ai-impacts-in-bls-employment-projections.htm', 'snippet': 'Therefore, credit analysts are likely to see decreasing employment demand, and their employment is projected to decline 3.9 percent from 2023 to 2033. (See ...', 'position': 6}, {'title': '60+ Stats On AI Replacing Jobs (2025) - Exploding Topics', 'link': 'https://explodingtopics.com/blog/ai-replacing-jobs', 'snippet': 'In May 2023, 3,900 US job losses were directly linked to AI (SEO.ai). Those 3,900 jobs represented 5% of the total jobs lost that month. In turn ...', 'position': 7}, {'title': 'The Impact of AI on Job Roles, Workforce, and Employment', 'link': 'https://www.innopharmaeducation.com/blog/the-impact-of-ai-on-job-roles-workforce-and-employment-what-you-need-to-know', 'snippet': 'According to a report by the World Economic Forum, by 2025, AI will have displaced 75 million jobs globally, but will have created 133 million new jobs. This ...', 'position': 8}, {'title': 'These Jobs Will Fall First As AI Takes Over The Workplace - Forbes', 'link': 'https://www.forbes.com/sites/jackkelly/2025/04/25/the-jobs-that-will-fall-first-as-ai-takes-over-the-workplace/', 'snippet': 'Goldman Sachs previously estimated that 300 million jobs could be lost to AI, affecting 25% of the global labor market. On the bright side, AI ...', 'position': 9}], 'peopleAlsoAsk': [{'question': 'How is AI affecting the job market?', 'snippet': 'How will artificial intelligence affect the workplace? While the logistics of some roles shift with the development of AI, many jobs will be enhanced rather than replaced. AI can automate repetitive tasks, freeing up employees to focus on more complex, creative or strategic work.', 'title': 'The Impact of AI on the Job Market and Employment Opportunities', 'link': 'https://onlinedegrees.sandiego.edu/ai-impact-on-job-market/'}, {'question': 'How many jobs will be lost to AI by 2025?', 'snippet': 'By 2025, two million workers in manufacturing could be replaced by automated tools (MIT / Boston University) Most of these automated tools are robots, not strictly AI, but some of these lost jobs will be replaced with new AI tools.\nApr 24, 2025', 'title': '60+ Stats On AI Replacing Jobs (2025) - Exploding Topics', 'link': 'https://explodingtopics.com/blog/ai-replacing-jobs'}, {'question': 'Is AI already shaking up the labor market?', 'snippet': '“Investment in AI is already changing the distribution of jobs in the economy.” The research also uncovered flat or declining employment specifically in low-paid service work.\nFeb 14, 2025', 'title': 'Is AI already shaking up labor market? - Harvard Gazette', 'link': 'https://news.harvard.edu/gazette/story/2025/02/is-ai-already-shaking-up-labor-market-a-i-artificial-intelligence/'}, {'question': 'How many jobs will AI replace by 2030?', 'snippet': 'Job Gains: The World Economic Forum forecasts that by 2030, 92 million jobs will be displaced by AI/automation globally, while 170 million new jobs will be created – a net gain of +78 million jobs (Future of Jobs Report 2025: The jobs of the future – and the skills you need to get them | World Economic Forum).', 'title': 'AI-Driven Agentification of Work: Impact on Jobs (2024–2030)', 'link': 'https://www.linkedin.com/pulse/ai-driven-agentification-work-impact-jobs-20242030-poweredbywiti-zbyfc'}], 'relatedSearches': [{'query': 'The impact of ai on job markets 2023 research paper'}, {'query': 'The impact of ai on job markets 2023 pdf'}], 'credits': 1}[00m



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
└── <span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🧠 </span><span style="color: #000080; text-decoration-color: #000080">Thinking...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    
    
    [1m[95m# Agent:[00m [1m[92mInternet Researcher[00m
    [95m## Final Answer:[00m [92m
    The impact of AI on job markets is extensive, characterized by both job displacement and the creation of new opportunities. Recent studies predict that AI and automation could displace millions of jobs while simultaneously creating new roles, underscoring the importance of ongoing skill development to adapt to these changes. The sources explored provide quantitative data and qualitative insights regarding these shifting dynamics across various sectors.[00m
    
    



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Task Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Task Completed</span>                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>                                                                     <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>                                                                                     <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: c0ca470d-8bcd-4c9a-938a-696f92ba7c05</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: c0ca470d-8bcd-4c9a-938a-696f92ba7c05</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[95m# Agent:[00m [1m[92mContent Summarizer[00m
    [95m## Task:[00m [92mSummarize the research report into a concise and informative paragraph. Ensure clarity, coherence, and completeness.[00m
    
    
    [1m[95m# Agent:[00m [1m[92mContent Summarizer[00m
    [95m## Final Answer:[00m [92m
    The impact of AI on job markets is profound, encompassing both the displacement of existing jobs and the emergence of new opportunities. Recent studies project that millions of jobs may be lost due to automation, yet these same technologies also have the potential to create new roles, emphasizing the critical need for continuous skill development to adjust to these evolving market conditions. The research incorporates both quantitative data and qualitative insights, highlighting the shifting dynamics across various sectors influenced by AI advancements.[00m
    
    



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: c0ca470d-8bcd-4c9a-938a-696f92ba7c05</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: c0ca470d-8bcd-4c9a-938a-696f92ba7c05</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Task Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Task Completed</span>                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">c0ca470d-8bcd-4c9a-938a-696f92ba7c05</span>                                                                     <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Agent: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>                                                                                      <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: c0ca470d-8bcd-4c9a-938a-696f92ba7c05</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: 8331277e-6432-4490-ac18-3d6af4ed0fd0</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: c0ca470d-8bcd-4c9a-938a-696f92ba7c05</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: 8331277e-6432-4490-ac18-3d6af4ed0fd0</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Fact-Checking Specialist</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[95m# Agent:[00m [1m[92mFact-Checking Specialist[00m
    [95m## Task:[00m [92mVerify the summarized information for accuracy using the SerperDevTool. Cross-check facts with reliable sources and correct any errors.[00m



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Fact-Checking Specialist</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    
    
    [1m[95m# Agent:[00m [1m[92mFact-Checking Specialist[00m
    [95m## Thought:[00m [92mI need to verify the summarized information regarding the impact of AI on job markets by checking reliable sources for accuracy and ensuring there are no misleading claims.[00m
    [95m## Using tool:[00m [92mSearch the internet with Serper[00m
    [95m## Tool Input:[00m [92m
    "{\"search_query\": \"impact of AI on job markets job displacement and creation opportunities 2023\"}"[00m
    [95m## Tool Output:[00m [92m
    {'searchParameters': {'q': 'impact of AI on job markets job displacement and creation opportunities 2023', 'type': 'search', 'num': 10, 'engine': 'google'}, 'organic': [{'title': 'The Impact of AI on Job Roles, Workforce, and Employment', 'link': 'https://www.innopharmaeducation.com/blog/the-impact-of-ai-on-job-roles-workforce-and-employment-what-you-need-to-know', 'snippet': 'While AI is creating new job opportunities, it is also leading to job displacement, particularly in industries that rely heavily on routine and repetitive tasks ...', 'position': 1}, {'title': '[PDF] Artificial Intelligence Impact on Labor Markets', 'link': 'https://www.iedconline.org/clientuploads/EDRP%20Logos/AI_Impact_on_Labor_Markets.pdf', 'snippet': "One of the primary concerns surrounding AI's impact on the labor market is the potential for widespread job displacement and automation. A ...", 'position': 2}, {'title': 'These Jobs Will Fall First As AI Takes Over The Workplace - Forbes', 'link': 'https://www.forbes.com/sites/jackkelly/2025/04/25/the-jobs-that-will-fall-first-as-ai-takes-over-the-workplace/', 'snippet': 'Goldman Sachs previously estimated that 300 million jobs could be lost to AI, affecting 25% of the global labor market. On the bright side, AI ...', 'position': 3}, {'title': 'Research: How Gen AI Is Already Impacting the Labor Market', 'link': 'https://hbr.org/2024/11/research-how-gen-ai-is-already-impacting-the-labor-market', 'snippet': 'Gen AI has the unique potential to impact all job sectors, particularly given its fundamental ability to improve its capabilities over time.', 'position': 4}, {'title': 'The Impact of Artificial Intelligence Application on Job Displacement ...', 'link': 'https://rsisinternational.org/journals/ijriss/articles/the-impact-of-artificial-intelligence-application-on-job-displacement-and-creation-a-systematic-review/', 'snippet': 'The International Monetary Fund (IMF 2024) report highlights that AI will impact 40% of global jobs, with many roles at risk of replacement.', 'position': 5}, {'title': '60+ Stats On AI Replacing Jobs (2025) - Exploding Topics', 'link': 'https://explodingtopics.com/blog/ai-replacing-jobs', 'snippet': 'In May 2023, 3,900 US job losses were directly linked to AI (SEO.ai). Those 3,900 jobs represented 5% of the total jobs lost that month. In turn ...', 'position': 6}, {'title': 'AI-Driven Agentification of Work: Impact on Jobs (2024–2030)', 'link': 'https://www.linkedin.com/pulse/ai-driven-agentification-work-impact-jobs-20242030-poweredbywiti-zbyfc', 'snippet': 'Job Losses Due to AI (2024–2030). Global Displacement Trends: AI and automation are expected to eliminate millions of jobs worldwide by 2030.', 'position': 7}, {'title': 'Jobs lost, jobs gained: What the future of work will mean ... - McKinsey', 'link': 'https://www.mckinsey.com/featured-insights/future-of-work/jobs-lost-jobs-gained-what-the-future-of-work-will-mean-for-jobs-skills-and-wages', 'snippet': 'Workers displaced by automation are easily identified, while new jobs that are created indirectly from technology are less visible and spread ...', 'position': 8}, {'title': 'AI Replacing Jobs Statistics: The Impact on Employment in 2025', 'link': 'https://seo.ai/blog/ai-replacing-jobs-statistics', 'snippet': '14% of workers have experienced job displacement due to AI, suggesting that the present impact is somewhat more restrained than the anticipation.', 'position': 9}], 'peopleAlsoAsk': [{'question': 'How will AI affect the job market and employment opportunities?', 'snippet': 'How will artificial intelligence affect the workplace? While the logistics of some roles shift with the development of AI, many jobs will be enhanced rather than replaced. AI can automate repetitive tasks, freeing up employees to focus on more complex, creative or strategic work.', 'title': 'The Impact of AI on the Job Market and Employment Opportunities', 'link': 'https://onlinedegrees.sandiego.edu/ai-impact-on-job-market/'}, {'question': 'How many jobs has AI replaced in 2023?', 'snippet': "14% of workers claim to have already lost a job to 'robots'. In May 2023, 3,900 US job losses were linked directly to AI.\nDec 2, 2024", 'title': 'AI Replacing Jobs Statistics: The Impact on Employment in 2025', 'link': 'https://seo.ai/blog/ai-replacing-jobs-statistics'}, {'question': 'How does artificial intelligence affect job displacement?', 'snippet': 'The Job Replacement Narrative: As AI continues to advance, it is expected to replace certain jobs that involve predictable, rule-based tasks. However, history tells us that technological advancements, despite initial job displacements, often lead to the creation of new, more specialized roles.', 'title': 'The Impact of Artificial Intelligence on Employment: Replacing Jobs or ...', 'link': 'https://sageuniversity.edu.in/blogs/impact-of-artificial-intelligence-on-employment'}, {'question': 'How will AI impact the job market in the next 5 10 years?', 'snippet': 'McKinsey Global Institute projections suggest automation could displace between 400 and 800 million jobs globally by 2030 (depending on adoption speed), forcing up to 375 million workers (14% of the global workforce) to change occupations (AI Job Displacements: UBI to the Rescue? - Seven Pillars Institute).\nFeb 28, 2025', 'title': 'AI-Driven Agentification of Work: Impact on Jobs (2024–2030)', 'link': 'https://www.linkedin.com/pulse/ai-driven-agentification-work-impact-jobs-20242030-poweredbywiti-zbyfc'}], 'relatedSearches': [{'query': 'Positive impact of ai on job markets job displacement and creation opportunities 2023'}, {'query': 'Negative impact of ai on job markets job displacement and creation opportunities 2023'}], 'credits': 1}[00m



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Fact-Checking Specialist</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
└── <span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🧠 </span><span style="color: #000080; text-decoration-color: #000080">Thinking...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Fact-Checking Specialist</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    
    
    [1m[95m# Agent:[00m [1m[92mFact-Checking Specialist[00m
    [95m## Final Answer:[00m [92m
    The impact of AI on job markets is profound and multifaceted, characterized by both the displacement of existing jobs and the emergence of new opportunities. According to research, AI and automation are projected to significantly affect the workforce, potentially displacing millions of jobs while simultaneously paving the way for new roles. Notably, a report by Goldman Sachs estimated that up to 300 million jobs could be lost to AI, affecting approximately 25% of the global labor market. Yet, these technologies also offer the potential for job creation, especially in sectors that require more advanced skills and competencies.
    
    Studies indicate that continuous skill development is crucial for workers to adapt to these transitions. The McKinsey Global Institute forecasts that automation could displace between 400 and 800 million jobs globally by 2030, depending on the rate of adoption, which could require around 375 million workers (14% of the global workforce) to change occupations. It's important to acknowledge that while job loss is a significant concern, historical patterns suggest that technological advancements often lead to the creation of new and more specialized positions as well.
    
    Research efforts show that AI is reshaping roles across various sectors, particularly in areas reliant on repetitive tasks. A survey indicated that 14% of workers reported experiencing job displacement due to AI, with specific figures noting that in May 2023, approximately 3,900 job losses in the U.S. could be directly attributed to automation technologies.
    
    The implications of these changes underscore the critical importance of ongoing skill development and education to help workers navigate the evolving job landscape influenced by advancements in AI technology.[00m
    
    



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: c0ca470d-8bcd-4c9a-938a-696f92ba7c05</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: 8331277e-6432-4490-ac18-3d6af4ed0fd0</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Fact-Checking Specialist</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 5e53c9c4-f7b6-4b32-b66b-22b892897f64</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Internet Researcher</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: c0ca470d-8bcd-4c9a-938a-696f92ba7c05</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
│   <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
│   └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Content Summarizer</span>
│       <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: 8331277e-6432-4490-ac18-3d6af4ed0fd0</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Fact-Checking Specialist</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Fact-Checking Specialist</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Task Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Task Completed</span>                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">8331277e-6432-4490-ac18-3d6af4ed0fd0</span>                                                                     <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Agent: </span><span style="color: #008000; text-decoration-color: #008000">Fact-Checking Specialist</span>                                                                                <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Crew Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Crew Execution Completed</span>                                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">crew</span>                                                                                                     <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008000; text-decoration-color: #008000">68ea02fd-d221-4e0c-bbe7-217b4b169e5a</span>                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




```python
from IPython.display import Markdown

Markdown(result.raw)
```




The impact of AI on job markets is profound and multifaceted, characterized by both the displacement of existing jobs and the emergence of new opportunities. According to research, AI and automation are projected to significantly affect the workforce, potentially displacing millions of jobs while simultaneously paving the way for new roles. Notably, a report by Goldman Sachs estimated that up to 300 million jobs could be lost to AI, affecting approximately 25% of the global labor market. Yet, these technologies also offer the potential for job creation, especially in sectors that require more advanced skills and competencies.

Studies indicate that continuous skill development is crucial for workers to adapt to these transitions. The McKinsey Global Institute forecasts that automation could displace between 400 and 800 million jobs globally by 2030, depending on the rate of adoption, which could require around 375 million workers (14% of the global workforce) to change occupations. It's important to acknowledge that while job loss is a significant concern, historical patterns suggest that technological advancements often lead to the creation of new and more specialized positions as well.

Research efforts show that AI is reshaping roles across various sectors, particularly in areas reliant on repetitive tasks. A survey indicated that 14% of workers reported experiencing job displacement due to AI, with specific figures noting that in May 2023, approximately 3,900 job losses in the U.S. could be directly attributed to automation technologies.

The implications of these changes underscore the critical importance of ongoing skill development and education to help workers navigate the evolving job landscape influenced by advancements in AI technology.



### Coming Ahead
- Building Agent that scales
- Creating and integrating custom tools.
- Agentic RAG
- Using Flows for Mulit agent coordinations.
- Agentic Patterns
