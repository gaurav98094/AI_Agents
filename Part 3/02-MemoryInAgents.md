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

### Define Agent, Task & Crew


```python
# Define a simple agent (assuming a default LLM agent)
assistant = Agent(
    role="Personal Assistant",
    goal="""You are a personal assistant that can help the user with their tasks.""",
    backstory="""You are a personal assistant that can help the user with their tasks.""",
    verbose=True
)

task = Task(
    description="Handle this task: {user_task}",
    expected_output="A clear and concise answer to the question.",
    agent=assistant
)

# Create a crew with memory enabled
crew = Crew(
    agents=[assistant], 
    tasks=[task], 
    process=Process.sequential,
    memory=True,                   # Enable memory for the crew
    verbose=True
)
```


```python
user_input = """My favorite color is #46778F and
                my favorite Agent framework is CrewAI."""

result = crew.kickoff(inputs={"user_task": user_input})

print(result)
```

    My favorite color is #46778F and my favorite Agent framework is CrewAI.



```python
# Test for memroy
user_input = """Tell me about my fav color?"""

result = crew.kickoff(inputs={"user_task": user_input})
print(result)
```

    My favorite color is #46778F.


### Let's explore a bit


```python
crew._short_term_memory
```




    ShortTermMemory(embedder_config=None, crew=None, storage=<crewai.memory.storage.rag_storage.RAGStorage object at 0x129b6a810>)




```python
crew._short_term_memory.search("What is my name?")
```




    [{'id': '811f61e8-d01c-4c90-ab94-d336e6c5a178',
      'metadata': {'agent': 'Personal Assistant',
       'observation': 'Handle this task: Tell me my name?'},
      'context': 'I now can give a great answer  \nFinal Answer: I do not have the information about your name. Please let me know your name so I can assist you better.',
      'score': 1.0544429682308243},
     {'id': '1c42b58c-a925-41ff-a7a1-35fcb825c1e1',
      'metadata': {'agent': 'Personal Assistant',
       'observation': 'Handle this task: Tell me about my fav color?'},
      'context': 'I now can give a great answer  \nFinal Answer: My favorite color is #46778F.',
      'score': 1.5027365687628105},
     {'id': '43208560-e59d-47c6-a3c6-e1f17feecd08',
      'metadata': {'agent': 'Personal Assistant',
       'observation': 'Handle this task: What is my favorite color?'},
      'context': 'I now can give a great answer  \nFinal Answer: My favorite color is #46778F and my favorite Agent framework is CrewAI.',
      'score': 1.505280258617871}]




```python
crew._long_term_memory
```




    LongTermMemory(embedder_config=None, crew=None, storage=<crewai.memory.storage.ltm_sqlite_storage.LTMSQLiteStorage object at 0x129af0650>)




```python

```
