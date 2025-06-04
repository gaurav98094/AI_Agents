
## 🧠 Knowledge Integration for AI Agents using CrewAI

In this guide, you'll learn how to enable AI agents to:

* 📁 Access a company knowledge base
* 📊 Query structured datasets like CSV or JSON
* 📄 Read and recall insights from PDFs, DOCs, and other documents
* ❓ Answer questions based on internal documentation


### 📌 What is "Knowledge for Agents"?

**Knowledge for Agents** refers to the **information and context required by an AI agent to reason, plan, and act intelligently**.

This knowledge may include:

* **Facts** – e.g., product specs, employee roles, pricing rules
* **Documents** – e.g., HR policies, SOPs, technical manuals
* **Tools** – e.g., APIs, databases (to interact with or query)
* **Memory** – e.g., past interactions, actions, or decisions
* **World Knowledge** – e.g., common sense, public information

> 💡 *Example:* If you're building a **travel booking agent**, its knowledge might include airline schedules, pricing APIs, visa regulations, and the user's trip history.

<br>

### 📌 Knowledge in CrewAI

CrewAI allows agents to use knowledge in two main ways:

##### 🔹 Agent-Level Knowledge

* Assigned directly to an agent.
* Ideal for *specialized roles* (e.g., a product assistant that knows only about product info).

##### 🔸 Crew-Level Knowledge

* Shared among multiple agents in the same crew.
* Suitable for *collaborative tasks* (e.g., marketing, support, and sales agents referencing the same product launch document).

📓 **Notebook**: `01 - Knowledge For Agents`

<br>

### 📌 Supported Knowledge Formats

You can load a variety of knowledge sources:

* `.txt`, `.pdf`, `.md`
* `.csv`, `.xlsx` (Excel)
* `.json`
* Custom APIs (via wrappers)
* Raw string input (e.g., from databases or internal tools)

<br>

### 📌 Example: Load Knowledge from a Text File

To load a `.txt` file as a knowledge source in CrewAI:

```python
from crewai.knowledge.source.text_file_knowledge_source import TextFileKnowledgeSource

text_source = TextFileKnowledgeSource(
    file_paths=["hr_policy.txt"]
)
```

<br>


### 📌 Knowledge vs Tools

| Concept       | Description                                                               |
| ------------- | ------------------------------------------------------------------------- |
| **Knowledge** | Passive information embedded in agents (e.g., policy docs, feature specs) |
| **Tools**     | Active components the agent can use in real time (e.g., APIs, databases)  |



### 📌 Use Cases

* A **support agent** referencing product FAQs or refund policies stored in PDF/Markdown.
* A **sales agent** accessing a shared CRM dump in `.csv` to answer customer queries.
* An **HR agent** parsing internal policy documents in `.docx` or `.txt`.


## 🧠 Memory For Agentic System
