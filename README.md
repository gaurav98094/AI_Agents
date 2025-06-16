
# 📘 Table of Contents


### **🧩 Part 1: Foundations of Agent Systems**

1. **Introduction**

2. **Motivation for Agents**
   * Perspective from Retrieval-Augmented Generation (RAG)
   * Perspective from Software Development
   * Perspective from Autonomous Systems

3. **Example Task: Research Report**
   * Approach Using a Basic LLM
   * Approach Using Agents

4. **Core Components of AI Agents**

5. **Designing Agent Architectures**

6.  **Building Agents**

7. **Structured Output**

   * Why Structured Output Matters
   * Using Pydantic for Structured Output

8. **Custom Tool Integration**
   * Implementing Custom Tools

9. **Agent Flows**

   * Why Flows Are Needed
   * Implementing Flows
   * Key Flow Concepts
     * State Management
     * State Handling in Flows
     * Router Logic

10. **Multi-Agent Coordination**
    * Working with Crews and Flows
    * Managing Multiple Crews

11. **🚀 Project Series**
    * Social Media Content Writer
    * Book Authoring Assistant

---

### **🚀 Part 2: Advanced Agent Workflows**

1. **Advanced Concepts Introduction**
   * Recap of Agent Capabilities, Flows, and Multi-Crew Coordination

2. **Guardrails**
   * Purpose and Benefits of Guardrails
   * Use Case: Legal Assistant
   * Writing Guardrail Functions
   * Return Format & Retry Logic
   * Guardrails in Action

3. **Referencing Task Outputs**
   * Using Previous Task Results Dynamically
   * Chaining Dependent Tasks
   * Task Output Referencing

4. **Asynchronous Execution**
   * Running Tasks in Parallel
   * When and How to Use Async Workflows
   * Async Task Execution

5. **Callbacks**
   * Post-Task Hooks and Automation
   * Examples: Notifications, Database Updates
   * Example Task with Callback

6. **Hierarchical Workflows**
   * Designing Nested Agent Systems
   * Use Cases for Orchestrator-Worker Patterns
   * Implementing Hierarchical Agents

7. **Human-in-the-Loop (HITL)**

   * Injecting Human Oversight
   * HITL in High-Stakes Domains
   * Implementing HITL Workflows

8. **Multimodal Agents**

   * Handling Text, Images, Audio, and More
   * Example Configuration for Multimodal Agents

--- 

### **🧩 Part 3**

1. **Knowledge Integration for AI Agents using CrewAI**
   * What is "Knowledge for Agents"?
   * Knowledge in CrewAI
     * Agent-Level Knowledge
     * Crew-Level Knowledge
   * Supported Knowledge Formats
   * Example: Load Knowledge from a Text File
   * Knowledge vs Tools
   * Use Cases

2. **Memory in Agentic Systems**
   * What is Memory?
   * Types of Memory
     * Short-Term Memory
     * Long-Term Memory
     * Entity Memory
     * Contextual Memory
     * User Memory
   * How Memory Works in CrewAI
   * Resetting Memory

---

### 📚 Part 4

1. **ReAct Agent**

   * Overview of Reasoning + Acting
   * Key Benefits of ReAct
   * Thought → Action → Observation Loop
   * 📓 Notebook: `01 - ReAct From Scratch`



2. **Planning Agents**
   * Overview of the Planning Pattern
   * Benefits of Pre-planned Execution
   * Two-phase Agentic Execution
     * Plan → Execute → Respond
   * 📓 Notebook: `02 - Planning Pattern From Scratch`