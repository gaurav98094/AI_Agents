## Implementing Flows



**Aim**: Build a task management systemm 
1. Generates a task for a software engineer.
2. Updates the task’s status to "In Progress."
3. Marks the task as "Completed."



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

### Using Unstructured State


```python
class TaskManagementFlow(Flow):

    @start()
    def generate_task(self):
        print(f"Flow started. State ID: {self.state['id']}")
        
        # Step 1: Generate a new task
        self.state["task"] = "Fix a critical bug in the payment system"
        self.state["status"] = "Pending"
        print(f"Task generated: {self.state['task']} (Status: {self.state['status']})")

    @listen(generate_task)
    def start_task(self):
        # Step 2: Update task status to 'In Progress'
        self.state["status"] = "In Progress"
        print(f"Task status updated: {self.state['status']}")

    @listen(start_task)
    def complete_task(self):
        # Step 3: Mark task as 'Completed'
        self.state["status"] = "Completed"
        print(f"Task status updated: {self.state['status']}")
        print(f"Final Task State: {self.state}")
```


```python
# Execute the flow
flow = TaskManagementFlow()
final_result = await flow.kickoff_async()
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080">╭──────────────────────────────────────────────── Flow Execution ─────────────────────────────────────────────────╮</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #000080; text-decoration-color: #000080; font-weight: bold">Starting Flow Execution</span>                                                                                        <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>                                                                                       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #000080; text-decoration-color: #000080">5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc</span>                                                                       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc</span>
└── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[35m Flow started with ID: 5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc[00m



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc</span>
├── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: generate_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Flow started. State ID: 5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc
    Task generated: Fix a critical bug in the payment system (Status: Pending)



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: start_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Task status updated: In Progress



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: start_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: start_task</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: complete_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Task status updated: Completed
    Final Task State: {'id': '5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc', 'task': 'Fix a critical bug in the payment system', 'status': 'Completed'}



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: start_task</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: complete_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Flow Finished: </span><span style="color: #008000; text-decoration-color: #008000">TaskManagementFlow</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: start_task</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: complete_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Flow Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Flow Execution Completed</span>                                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">TaskManagementFlow</span>                                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008000; text-decoration-color: #008000">5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc</span>                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




```python
flow.state
```




    {'id': '5cdd8dfc-d2a3-4a96-90ad-ce2d87a6d0bc',
     'task': 'Fix a critical bug in the payment system',
     'status': 'Completed'}



### Structured State


```python
from pydantic import BaseModel

class TaskState(BaseModel):
    task: str = None
    status: str = None
```


```python
class TaskManagementFlow(Flow[TaskState]):

    @start()
    def generate_task(self):
        print(f"Flow started. State ID: {self.state.id}")
        
        # Step 1: Generate a new task
        self.state.task = "Fix a critical bug in the payment system"
        self.state.status = "Pending"
        print(f"Task generated: {self.state.task} (Status: {self.state.status})")

    @listen(generate_task)
    def start_task(self):
        # Step 2: Update task status to 'In Progress'
        self.state.status = "In Progress"
        print(f"Task status updated: {self.state.status}")

    @listen(start_task)
    def complete_task(self):
        # Step 3: Mark task as 'Completed'
        self.state.status = "Completed"
        print(f"Task status updated: {self.state.status}")
        print(f"Final Task State: {self.state}")
```


```python
# Execute the flow
flow = TaskManagementFlow()
final_result = await flow.kickoff_async()
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080">╭──────────────────────────────────────────────── Flow Execution ─────────────────────────────────────────────────╮</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #000080; text-decoration-color: #000080; font-weight: bold">Starting Flow Execution</span>                                                                                        <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>                                                                                       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #000080; text-decoration-color: #000080">b1136ed9-ddf3-4617-91c0-94078d10bdb8</span>                                                                       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">b1136ed9-ddf3-4617-91c0-94078d10bdb8</span>
└── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[35m Flow started with ID: b1136ed9-ddf3-4617-91c0-94078d10bdb8[00m



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">b1136ed9-ddf3-4617-91c0-94078d10bdb8</span>
├── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: generate_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Flow started. State ID: b1136ed9-ddf3-4617-91c0-94078d10bdb8
    Task generated: Fix a critical bug in the payment system (Status: Pending)



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">b1136ed9-ddf3-4617-91c0-94078d10bdb8</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">b1136ed9-ddf3-4617-91c0-94078d10bdb8</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: start_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Task status updated: In Progress



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">b1136ed9-ddf3-4617-91c0-94078d10bdb8</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: start_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">b1136ed9-ddf3-4617-91c0-94078d10bdb8</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: start_task</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: complete_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Task status updated: Completed
    Final Task State: id='b1136ed9-ddf3-4617-91c0-94078d10bdb8' task='Fix a critical bug in the payment system' status='Completed'



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TaskManagementFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">b1136ed9-ddf3-4617-91c0-94078d10bdb8</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: start_task</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: complete_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Flow Finished: </span><span style="color: #008000; text-decoration-color: #008000">TaskManagementFlow</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: generate_task</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: start_task</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: complete_task</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Flow Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Flow Execution Completed</span>                                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">TaskManagementFlow</span>                                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008000; text-decoration-color: #008000">b1136ed9-ddf3-4617-91c0-94078d10bdb8</span>                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




```python
flow.state
```




    StateWithId(id='b1136ed9-ddf3-4617-91c0-94078d10bdb8', task='Fix a critical bug in the payment system', status='Completed')



### Conditional Flow


```python
# OR Conditional Flow Execution

from crewai.flow.flow import Flow, listen, or_, start

class SupportFlow(Flow):
    @start()
    def live_chat_request(self):
        return "Support request received via live chat"

    @start()
    def email_ticket_request(self):
        return "Support request received via email ticket"

    @listen(or_(live_chat_request, email_ticket_request))
    def log_request(self, request_source):
        print(f"Logging request: {request_source}")

```


```python
# Execute the flow
flow = SupportFlow()
final_result = await flow.kickoff_async()
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080">╭──────────────────────────────────────────────── Flow Execution ─────────────────────────────────────────────────╮</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #000080; text-decoration-color: #000080; font-weight: bold">Starting Flow Execution</span>                                                                                        <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>                                                                                              <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>                                                                       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>
└── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[35m Flow started with ID: 74b4dc83-5896-4e9d-8b8e-8c6acebee756[00m



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>
├── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: live_chat_request</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: live_chat_request</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: live_chat_request</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: email_ticket_request</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: live_chat_request</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: email_ticket_request</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: live_chat_request</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: email_ticket_request</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: log_request</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Logging request: Support request received via live chat



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: live_chat_request</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: email_ticket_request</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: log_request</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: live_chat_request</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: email_ticket_request</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: log_request</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Logging request: Support request received via email ticket



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">SupportFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: live_chat_request</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: email_ticket_request</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: log_request</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Flow Finished: </span><span style="color: #008000; text-decoration-color: #008000">SupportFlow</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: live_chat_request</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: email_ticket_request</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: log_request</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Flow Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Flow Execution Completed</span>                                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">SupportFlow</span>                                                                                              <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008000; text-decoration-color: #008000">74b4dc83-5896-4e9d-8b8e-8c6acebee756</span>                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




```python
## AND Conditional Flow Execution
from crewai.flow.flow import Flow, and_, listen, start

class TicketEscalationFlow(Flow):

    @start()
    def user_confirms_issue(self):
        self.state["user_confirmation"] = True
        print("User confirmed they still need assistance.")

    @listen(user_confirms_issue)
    def agent_reviews_ticket(self):
        self.state["agent_review"] = True
        print("Support agent has reviewed the ticket.")

    @listen(and_(user_confirms_issue, agent_reviews_ticket))
    def escalate_ticket(self):
        print("Escalating ticket to Level 2 support!")
    
```


```python
# Execute the flow
flow = TicketEscalationFlow()
final_result = await flow.kickoff_async()
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080">╭──────────────────────────────────────────────── Flow Execution ─────────────────────────────────────────────────╮</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #000080; text-decoration-color: #000080; font-weight: bold">Starting Flow Execution</span>                                                                                        <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #000080; text-decoration-color: #000080">TicketEscalationFlow</span>                                                                                     <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #000080; text-decoration-color: #000080">ec1e63e1-ef7f-4751-8366-92ecdaf4bf46</span>                                                                       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TicketEscalationFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">ec1e63e1-ef7f-4751-8366-92ecdaf4bf46</span>
└── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[35m Flow started with ID: ec1e63e1-ef7f-4751-8366-92ecdaf4bf46[00m



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TicketEscalationFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">ec1e63e1-ef7f-4751-8366-92ecdaf4bf46</span>
├── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: user_confirms_issue</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    User confirmed they still need assistance.



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TicketEscalationFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">ec1e63e1-ef7f-4751-8366-92ecdaf4bf46</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: user_confirms_issue</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TicketEscalationFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">ec1e63e1-ef7f-4751-8366-92ecdaf4bf46</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: user_confirms_issue</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: agent_reviews_ticket</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Support agent has reviewed the ticket.



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TicketEscalationFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">ec1e63e1-ef7f-4751-8366-92ecdaf4bf46</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: user_confirms_issue</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: agent_reviews_ticket</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TicketEscalationFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">ec1e63e1-ef7f-4751-8366-92ecdaf4bf46</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: user_confirms_issue</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: agent_reviews_ticket</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: escalate_ticket</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Escalating ticket to Level 2 support!



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TicketEscalationFlow</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">ec1e63e1-ef7f-4751-8366-92ecdaf4bf46</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: user_confirms_issue</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: agent_reviews_ticket</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: escalate_ticket</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Flow Finished: </span><span style="color: #008000; text-decoration-color: #008000">TicketEscalationFlow</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: user_confirms_issue</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: agent_reviews_ticket</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: escalate_ticket</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Flow Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Flow Execution Completed</span>                                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">TicketEscalationFlow</span>                                                                                     <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008000; text-decoration-color: #008000">ec1e63e1-ef7f-4751-8366-92ecdaf4bf46</span>                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



### Router Logic

Aim : Assign Urgent ticker to live customer support


```python
from pydantic import BaseModel
import random

class TickerState(BaseModel):
    priority: str = "low"
```


```python
from crewai.flow.flow import Flow, listen, router, start


class TickerRouting(Flow[TickerState]):

    @start()
    def classify_ticker(self):
        print("Classifying ticket priority...")
        self.state.priority = random.choice(["low", "high"])
        print(f"Ticket classified as {self.state.priority} priority.")

    @router(classify_ticker)
    def route_ticker(self):
        if self.state.priority == "high":
            return "Urgent Support"
        else:
            return "Email Support"
        
    @listen("urgent_support")
    def assign_to_agent(self):
        print("Assigning high priority ticket to an agent.")

    @listen("email_support")
    def send_to_email_queue(self):
        print("Sending low priority ticket to email queue.")
```


```python
# Execute the flow
flow = TickerRouting()
final_result = await flow.kickoff_async()
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080">╭──────────────────────────────────────────────── Flow Execution ─────────────────────────────────────────────────╮</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #000080; text-decoration-color: #000080; font-weight: bold">Starting Flow Execution</span>                                                                                        <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #000080; text-decoration-color: #000080">TickerRouting</span>                                                                                            <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #000080; text-decoration-color: #000080">cb55fd21-d340-4de3-9580-c854cac57b89</span>                                                                       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TickerRouting</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">cb55fd21-d340-4de3-9580-c854cac57b89</span>
└── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    [1m[35m Flow started with ID: cb55fd21-d340-4de3-9580-c854cac57b89[00m



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TickerRouting</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">cb55fd21-d340-4de3-9580-c854cac57b89</span>
├── <span style="color: #808000; text-decoration-color: #808000">🧠 Starting Flow...</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: classify_ticker</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>



    Classifying ticket priority...
    Ticket classified as high priority.



<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TickerRouting</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">cb55fd21-d340-4de3-9580-c854cac57b89</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: classify_ticker</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TickerRouting</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">cb55fd21-d340-4de3-9580-c854cac57b89</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: classify_ticker</span>
└── <span style="color: #808000; text-decoration-color: #808000; font-weight: bold">🔄 Running: route_ticker</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">🌊 Flow: </span><span style="color: #000080; text-decoration-color: #000080">TickerRouting</span>
<span style="color: #c0c0c0; text-decoration-color: #c0c0c0">    ID: </span><span style="color: #000080; text-decoration-color: #000080">cb55fd21-d340-4de3-9580-c854cac57b89</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: classify_ticker</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: route_ticker</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Flow Finished: </span><span style="color: #008000; text-decoration-color: #008000">TickerRouting</span>
├── <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Flow Method Step</span>
├── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: classify_ticker</span>
└── <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">✅ Completed: route_ticker</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008000; text-decoration-color: #008000">╭──────────────────────────────────────────────── Flow Completion ────────────────────────────────────────────────╮</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #008000; text-decoration-color: #008000; font-weight: bold">Flow Execution Completed</span>                                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">Name: </span><span style="color: #008000; text-decoration-color: #008000">TickerRouting</span>                                                                                            <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>  <span style="color: #c0c0c0; text-decoration-color: #c0c0c0">ID: </span><span style="color: #008000; text-decoration-color: #008000">cb55fd21-d340-4de3-9580-c854cac57b89</span>                                                                       <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">│</span>                                                                                                                 <span style="color: #008000; text-decoration-color: #008000">│</span>
<span style="color: #008000; text-decoration-color: #008000">╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>




<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace">
</pre>




```python
flow.plot()
```

    Warning: No node found for 'urgent_support' or 'assign_to_agent'. Skipping edge.
    Warning: No node found for 'email_support' or 'send_to_email_queue'. Skipping edge.
    Plot saved as crewai_flow.html

