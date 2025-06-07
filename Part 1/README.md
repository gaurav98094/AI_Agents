# AI Agents
<img src="img/image1.png">


## 📘 Table of Contents


### **🧩 Part 1: Foundations of Agent Systems**

1. **Introduction**
2. **Motivation for Agents**
3. **Example Task: Research Report**
4. **Core Components of AI Agents**
5. **Designing Agent Architectures**
6. **Building First Agents**
7. **Structured Output**
8. **Custom Tool Integration**
9. **Agent Flows**
10. **Multi-Agent Coordination**
11. **🚀 Project Series**


## Motivation for Agents

**From the RAG Perspective**

* RAG (Retrieval-Augmented Generation) works well but follows a fixed process: set steps → search database → generate response.
* AI Agents are smarter systems that can think, plan, and find useful information on their own.

**From the Software Development Perspective**

* Traditional systems are rigid and follow strict rules.
* Agents can handle tasks flexibly and adapt to new situations.
* Multiple agents can work together to reach a shared goal.

**From the Autonomous System Perspective**

* Instead of just answering questions one by one, agents break big problems into smaller tasks and complete them step-by-step.



## Example Task

**Goal:** Create a report on the latest AI research trends.

**Using a Normal LLM:**

* Ask for a summary of new AI research papers.
* Realize you need to check sources.
* Request a list of papers with references.
* Notice some sources are old, so ask again with better questions.
* After several tries, get a useful summary.

**Using Agents:**

* A *Research Agent* finds recent AI papers on sites like arXiv or Google Scholar.
* A *Filtering Agent* picks the best papers based on date, popularity, and keywords.
* A *Summarizing Agent* writes a clear report highlighting key points.
* A *Formatting Agent* arranges the report neatly and professionally.



## Key Parts of AI Agents

AI agents work by thinking, planning, and acting on their own. These are the six key parts that make them smart and dependable:

1. **Clear Roles:** Give each agent a clear and specific job. This helps get better results.
2. **Focused Tasks:** Each agent should handle one task at a time to avoid mistakes.
3. **Right Tools:** Provide agents with the tools they need, but don’t overload them.
4. **Teamwork:** Different agents with different skills work together better than one agent doing everything.
5. **Rules and Limits:** Set boundaries so agents don’t make errors or get stuck in loops.
6. **Memory:** Use short-term and long-term memory to remember what’s important.



## How to Design Agent Systems

Think of building an agent system like managing a team:

* **Set the Goal:** What do you want the agent to achieve?
* **Plan the Steps:** How should the agent reach the goal efficiently?
* **Choose Experts:** What kind of specialists would do this job well?
* **Give Tools:** What resources do these experts need to do their work?

For example, instead of a generic “researcher,” create a “Market Research Analyst who knows AI trends.” Instead of a simple “writer,” have a “Senior Technical Content Strategist.”

By giving agents clear roles, goals, and tools, you help them work better and deliver higher quality results. Being specific is very important.


📓 **Refer to Notebook 01: Building Agents**

* Use **CrewAI** to create agents.
* Build a **multi-agent system** where each agent has a specific role.
* Equip agents with **tools** to help them perform tasks effectively.



### 📦 Structured Output

LLMs usually return plain text, but for real-world applications, we often need **structured and predictable outputs**.

Why is structure important?

* APIs and systems need data in a fixed format to work correctly.
* A consistent structure helps extract key insights easily and reliably.



### ✅ How to Get Structured Output?

Use **Pydantic** to define data models that ensure the LLM responses follow a clear format.



📓 **Refer to Notebook 02: Structured Output with Pydantic**

* Learn how to use **Pydantic** with LLMs.
* Ensure responses match a defined schema.
* Easily parse and validate the output.



### 🛠️ Custom Tools

Agents can also use custom tools to extend their capabilities.

📓 **Refer to Notebook 03: Using Custom Tools**

* Example: Build a **custom currency conversion tool** that agents can use during their tasks.


## Flows

**Flows** are a powerful feature designed to streamline the creation, orchestration, and management of AI workflows. They enable the development of structured, event-driven processes, while allowing for effective state management and controlled execution flow within AI-driven systems.


### 🔍 Why Use Flows?

* Allowing LLMs to operate without structure can lead to unpredictable or undesired behavior.
* **Flows** help enforce structured logic while preserving AI autonomy.
* They provide infrastructure that bridges traditional software engineering principles with the flexible decision-making capabilities of AI.

📓 **Refer to Notebook 04: Implementing Flows**


### 🧠 Key Concepts to Remember

* `@start()`:
  Marks the entry point(s) of your Flow. Multiple methods can be decorated with `@start()` and will run concurrently.

* `@listen(task_name)`:
  Makes a task wait for another task (identified by `task_name`) to complete, and uses its output as input.

* **Flow State**:
  Every Flow has a `state` attribute which stores shared data throughout the workflow. This can be accessed via:

  ```python
  flow.state
  ```


### 🧾 State Management in Flows

Managing state is critical in AI workflows for maintaining consistency and context.

* **Unstructured State**:

  * Flexible and dynamic
  * No predefined schema
  * Suitable for experimental or loosely defined workflows

* **Structured State**:

  * Enforces schema validation using a model-based approach
  * Ideal for production-ready systems that require reliability and traceability

📓 **Refer to Notebook 05: State in Flows**


### 🔁 Router Logic

* `@router`:
  This decorator enables conditional branching within a Flow. It decides which task to run next based on the current context or output of a previous task.


### 👥 Crews with Flows

Now that you understand Flows, let’s see how to integrate them with **Crews** to build more complex, collaborative, agent-based workflows.

📓 **Refer to Notebook 06: Crews With Flows**

To create a new Flow, use the CLI:

```bash
crewai create flow test_flow
```

### Dealing With Muliple Crew
- In realworld single crew will not be enough.
- Crew must collaborate, share information and have optimized workflows.


### Project Time
Aim : Build Social Media Content Writer Project

**Working**
- Provide link to blog.
- Use FireCrawl to scrape the blog with images and save as markdown.
- Access the existing social content and understand writing style.
- Publish content to LinkedLn or X. Make use of routers in workflow.
- Write ready to publish draft.
- Save the content plan as a structured json file.