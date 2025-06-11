# Memory In Agents

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
import nest_asyncio
nest_asyncio.apply()
```


```python
from crewai import Crew, Agent, Task, Process
```

## Short-Term Momory



```python
from crewai import Crew, Agent, Task, Process
from crewai.memory import ShortTermMemory
from crewai.memory.storage.rag_storage import RAGStorage

shared_db = "./short_term_memory.db"

storage = RAGStorage(path=shared_db, type="short_term")

short_term_memory = ShortTermMemory(storage=storage)
```


```python
agent = Agent(
    role="A Personal Assistant",
    goal="""You are a personal assistant that can
            help the user with their tasks.""",
    backstory="""You are a personal assistant that
                can help the user with their tasks.""",
    verbose=True
)

task = Task(
    description="Handle this task: {user_task}",
    expected_output="A clear and concise answer to the question.",
    agent=agent
)


crew = Crew(
    agents=[agent], 
    tasks=[task], 
    process=Process.sequential,
    memory=True,
    short_term_memory=short_term_memory     # Define the short term memory
)

crew.kickoff(inputs={"user_task": "My favorite color is #46778F."})
```

## Long-Term Memory



```python
from crewai import Crew, Agent, Task, Process
from crewai.memory import LongTermMemory
from crewai.memory.storage.ltm_sqlite_storage import LTMSQLiteStorage
```


```python
shared_db = "./agent_memory.db"

storage = LTMSQLiteStorage(db_path=shared_db)

long_memory = LongTermMemory(storage=storage)
```


```python
agent = Agent(
    role="A Personal Assistant",
    goal="""You are a personal assistant that can
            help the user with their tasks.""",
    backstory="""You are a personal assistant that
                can help the user with their tasks.""",
    verbose=True
)

task = Task(
    description="Handle this task: {user_task}",
    expected_output="A clear and concise answer to the question.",
    agent=agent
)


crew = Crew(
    agents=[agent], 
    tasks=[task], 
    process=Process.sequential,
    memory=True,
    long_term_memory=long_memory    # Define the long term memory
)

crew.kickoff(inputs={"user_task": "My favorite color is #46778F."})
```
