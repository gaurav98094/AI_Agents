# Knowledge For Agents

### Setup


```python
# !pip install crewai
# !pip install crewai-tools


# Installing it to see traces(Found some issues with passing knowledge at crew level)
# !pip install langtrace-python-sdk
```


```python
# ollama pull llama3.2:1b
```

### Imports


```python
from dotenv import load_dotenv
import os

load_dotenv()
```




    True




```python
from crewai.knowledge.source.string_knowledge_source import StringKnowledgeSource

from crewai import Agent, Task, Crew, Process
```


```python
from langtrace_python_sdk import langtrace
from langchain_openai import ChatOpenAI

# Define OpenAI LLM
llm = ChatOpenAI(
    model="gpt-4",
    temperature=0.7
)

langtrace.init(api_key = os.environ.get('LANGTRACE_API_KEY'))
```

    [32mInitializing Langtrace SDK..[39m
    [37m⭐ Leave our github a star to stay on top of our updates - https://github.com/Scale3-Labs/langtrace[39m
    [34mExporting spans to Gaurav Kandel..[39m
    [34mLangtrace Project URL: https://app.langtrace.ai/project/cmbib9ry1002pbk2m5r68eixs/traces[39m


### Define Knowledge For Agent


```python
policy_text = """
Our return policy allows customers to return
any product within 30 days of purchase. Refunds
will be issued only if the item is unused and in original packaging.
Customers must provide proof of purchase when requesting a return.
"""

# Create a StringKnowledgeSource object
return_policy_knowledge = StringKnowledgeSource(content=policy_text)
```

### Define Agent, Task & Crew


```python
returns_agent = Agent(
    role = "Product Returns Assistant",
    goal = "Answer customer questions about return policy accurately.",
    backstory = """You work in customer service and specialize
                 in returns, refunds, and policies.""",
    allow_delegation = False,
    # knowledge_sources = [return_policy_knowledge],
    verbose = True,
    llm = "gpt-4o",
    # llm=llm,
    # callback_manager = langtrace
)
```


```python
returns_task = Task(
    description = "Answer the customer question: {question}",
    expected_output = "A concise and accurate answer.",
    agent = returns_agent
)
```


```python
crew = Crew(
    agents = [returns_agent],
    tasks = [returns_task],
    process = Process.sequential,
    knowledge_sources = [return_policy_knowledge],
    verbose = True,
    # callback_manager = langtrace
)
```

    [91m 
    [2025-06-05 01:06:20][ERROR]: Failed to upsert documents: ValidationError.__new__() missing 1 required positional argument: 'line_errors'[00m
    [93m 
    [2025-06-05 01:06:20][WARNING]: Failed to init knowledge: ValidationError.__new__() missing 1 required positional argument: 'line_errors'[00m



```python
query = "Can I get a refund if I used the item once?"

result = crew.kickoff(inputs = {"question": query})
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080">╭──────────────────────────────────────────── Crew Execution Started ─────────────────────────────────────────────╮</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>                                                                                                                 <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>  <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">Crew Execution Started</span>                                                                                         <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008080; text-decoration-color: #008080">crew</span>                                                                                                     <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008080; text-decoration-color: #008080">0ad84af9-a9f8-483a-a413-9a1d1c844021</span>                                                                       <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>                                                                                                                 <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">│</span>                                                                                                                 <span style="color: #008080; text-decoration-color: #008080">│</span>
<span style="color: #008080; text-decoration-color: #008080">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: b6a995b8-605c-44a2-bb37-89fd1748690c</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: b6a995b8-605c-44a2-bb37-89fd1748690c</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Product Returns Assistant</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">In Progress</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[95m# Agent:[00m [1m[92mProduct Returns Assistant[00m
    [95m## Task:[00m [92mAnswer the customer question: Can I get a refund if I used the item once?[00m
    
    
    [1m[95m# Agent:[00m [1m[92mProduct Returns Assistant[00m
    [95m## Final Answer:[00m [92m
    Whether or not you can receive a refund for an item you have used once largely depends on the specific return policy of the store or company from which you purchased the item. Typically, many retailers have a return policy that allows for returns and refunds within a certain time frame even if the item has been used, as long as it is in its original condition and packaging. However, some items, particularly those involving personal use and hygiene, may not be eligible for return once used. For a definitive answer, it's best to refer to the specific return policy of the retailer or contact their customer service directly for clarification.[00m
    
    



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">📋 Task: b6a995b8-605c-44a2-bb37-89fd1748690c</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #bfbf7f; text-decoration-color: #bfbf7f">Executing Task...</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Product Returns Assistant</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">🚀 Crew: crew</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">📋 Task: b6a995b8-605c-44a2-bb37-89fd1748690c</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Assigned to: </span><span style="color: #008000; text-decoration-color: #008000">Product Returns Assistant</span>
    <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">   Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
    └── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">🤖 Agent: </span><span style="color: #008000; text-decoration-color: #008000">Product Returns Assistant</span>
        <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    Status: </span><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Task Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Task Completed</span>                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">b6a995b8-605c-44a2-bb37-89fd1748690c</span>                                                                     <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Agent: </span><span style="color: #008000; text-decoration-color: #008000">Product Returns Assistant</span>                                                                               <span style="color: #008000; text-decoration-color: #008000">│</span>
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
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008000; text-decoration-color: #008000">0ad84af9-a9f8-483a-a413-9a1d1c844021</span>                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




```python
crew.knowledge
```


```python
returns_agent.knowledge
```




    Knowledge(sources=[StringKnowledgeSource(chunk_size=4000, chunk_overlap=200, chunks=[], chunk_embeddings=[], storage=None, metadata={}, collection_name=None, content='\nOur return policy allows customers to return\nany product within 30 days of purchase. Refunds\nwill be issued only if the item is unused and in original packaging.\nCustomers must provide proof of purchase when requesting a return.\n')], storage=<crewai.knowledge.storage.knowledge_storage.KnowledgeStorage object at 0x166021990>, embedder=None, collection_name=None)




```python
from IPython.display import Markdown
Markdown(result.raw)
```




Whether you can receive a refund for an item you've used once depends on our return policy. Generally, if the item is in a resalable condition and returned within the specified return period with the original receipt, you may be eligible for a refund. However, some items may have specific restrictions or exceptions. Please check our detailed return policy or contact customer service for product-specific return information.


