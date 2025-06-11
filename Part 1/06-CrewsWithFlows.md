## Crews With Flows



```python
# !pip install crewai
# !pip install crewai-tools
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
### Go to directory test_flow
```


```python
from random import randint
from crewai.flow import Flow, listen, start

from pydantic import BaseModel

class PoemState(BaseModel):
    sentence_count: int = 1
    poem: str = ""

    
class PoemFlow(Flow[PoemState]):

    @start()
    def generate_sentence_count(self):
        print("Generating sentence count")
        self.state.sentence_count = randint(1, 5)
        
    @listen(generate_sentence_count)
    def generate_poem(self):
        result = PoemCrew().crew().kickoff(
            inputs={"sentence_count": self.state.sentence_count}
        )
        self.state.poem = result.raw
    
    @listen(generate_poem)
    def save_poem(self):
        print("Saving poem")
        with open("poem.txt", "w") as f:
            f.write(self.state.poem)
```
