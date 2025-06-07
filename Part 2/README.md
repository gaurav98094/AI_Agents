## 📘 Table of Contents

1. **Advanced Concepts Introduction**
2. **Guardrails**
3. **Referencing Task Outputs**
4. **Asynchronous Execution**
5. **Callbacks**
6. **Hierarchical Workflows**
7. **Human-in-the-Loop (HITL)**
8. **Multimodal Agents**


# 🧠 Advanced Agent Workflows with CrewAI

In the previous section, we explored:

* ✅ **Agent Capabilities**: Integrating agents with custom tools
* 🔁 **Flows**: Creating structured, event-driven workflows
* 🤝 **Multi-Crew Flows**: Coordinating multiple agents across different workflows

---

## 🚀 This Section Covers: Advanced Agent Concepts

We now delve deeper into powerful capabilities that elevate agent-based applications:

* 🛡️ **Guardrails**: Enforce output constraints and safety checks
* 🔗 **Referencing Task Outputs**: Dynamically use results from previous tasks
* ⚙️ **Asynchronous Execution**: Maximize throughput by running tasks in parallel
* 🔄 **Callbacks**: Post-task triggers for downstream actions
* 👨‍⚖️ **Human-in-the-Loop**: Add manual review and approval
* 🧱 **Hierarchical Agents**: Compose agents within agents
* 🖼️ **Multimodal Agents**: Handle text, images, audio, and more

---

## 🛡️ Guardrails: Constraining Agent Behavior

AI agents can be powerful but unpredictable. Guardrails ensure safety, reliability, and accuracy by enforcing rules on outputs.

### 🔒 Why Use Guardrails?

* **Prevent API overuse or irrelevant queries**
* **Ensure outputs meet validation criteria**
* **Fallback strategies on failure**

### 🏛️ Example (Legal Assistant):

Guardrails can:

* Prevent hallucinating legal facts
* Catch jurisdiction misinterpretations
* Block outdated precedent citations

---

## ✅ Example: Guardrail Function

Let’s say we want an agent that summarizes research papers **under 150 words**:

```python
def validate_summary_length(task_output):
    try:
        print("Validating summary length")
        task_str_output = str(task_output)
        total_words = len(task_str_output.split())

        print(f"Word count: {total_words}")

        if total_words > 150:
            return (False, f"Summary exceeds 150 words. Word count: {total_words}")

        if total_words == 0:
            return (False, "Generated summary is empty.")

        return (True, task_output)

    except Exception as e:
        return (False, f"Validation system error: {str(e)}")
```

### 🧪 Guardrail Return Format

```python
(True, validated_output)  # Success
(False, error_message)    # Validation failed
```

### 🧠 Task With Guardrail

```python
summary_task = Task(
    description="Summarize a research paper in 150 words.",
    expected_output="A concise research summary in 150 words.",
    agent=summary_agent,
    guardrail=validate_summary_length,
    max_retries=3
)
```

If validation fails, the task retries up to 3 times before failing.

📓 **Notebook**: `01_guardrails.ipynb`

---

## 🔗 Referencing Tasks & Outputs

Learn how to:

* Access results of previous tasks using `TaskOutput`
* Chain tasks where later steps depend on earlier outputs

📓 **Notebook**: `02_reference_tasks_outputs.ipynb`

---

## ⚙️ Asynchronous Task Execution

Run tasks **in parallel** to speed up workflows and reduce latency.

Use this when tasks are **independent** and don’t rely on each other’s outputs.

📓 **Notebook**: `03_async_execution.ipynb`

---

## 🔄 Callbacks: Post-Task Actions

Use callbacks to:

* Store results in a database
* Send alerts (e.g., Slack, email)
* Trigger follow-up tasks or scripts

### 💡 Example

```python
research_news_task = Task(
    description="Find and summarize the latest AI breakthroughs",
    expected_output="A structured summary of AI news headlines.",
    agent=research_agent,
    callback=notify_team
)
```

## 🧱 Hierarchical Agentic Workflows

Create **composable agent stacks** where one agent orchestrates multiple sub-agents.

Useful for:

* Complex planning
* Delegated problem solving

📓 **Notebook**: `04_hierarchical_agents.ipynb`

## 👨‍💼 Human-in-the-Loop (HITL)

Inject human feedback, approvals, or manual corrections between task steps.

Use cases:

* Legal review
* Medical decisions
* Any high-risk domain

📓 **Notebook**: `05_human_in_loop.ipynb`


---

## 🖼️ Multimodal Agents

Extend your agents to handle:

* 📄 Text
* 🖼️ Images
* 🔊 Audio
* 📊 Tables or PDFs

Enable richer interactions beyond plain language.

```python
from crewai import Agent, LLM

llm = LLM(model="gpt-4o")

quality_inspector = Agent(
    role="Product Quality Inspector",
    goal="Analyze and assess the quality of product images",
    backstory="""An experienced manufacturing quality control
                 expert who specializes in detecting defects
                 and ensuring compliance.""",
    multimodal=True,
    verbose=True,
    llm=llm
)
```