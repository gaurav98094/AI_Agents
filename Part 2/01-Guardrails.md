### Guardails For Structured Output


```python
from pydantic import BaseModel

class ResearchReport(BaseModel):
    """Represents a structured research report"""
    title: str
    summary: str
    key_findings: list[str]
```


```python
import json
from typing import Tuple, Any

def validate_json_report(task_output):
    """"""
    try:
        # Parse JSON output
        data = json.loads(task_output.pydantic.model_dump_json())

        # Check required fields
        if "title" not in data or "summary" not in data or "key_findings" not in data:
            return (False, "Missing required fields: title, summary, or key_findings.")

        return (True, task_output)
        
    except json.JSONDecodeError:
        return (False, "Invalid JSON format. Please ensure correct syntax.")
```

### Create Agent & Tasks


```python
from crewai import Agent

# Create the AI Agent
research_report_agent = Agent(
    role="Research Analyst",
    goal="Generate structured JSON reports for research papers",
    backstory="You are an expert in structured reporting.",
    verbose=False)


from crewai import Task

research_report_task = Task(
    description="Generate a structured JSON research report",
    expected_output="A JSON with 'title', 'summary', and 'key_findings'.",
    agent=research_report_agent,
    output_pydantic=ResearchReport,
    guardrail=validate_json_report,
    max_retries=3
)
```


```python

```
