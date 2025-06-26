# LangGraph Practice Notebooks

This repository contains two Jupyter notebooks demonstrating fundamental concepts and practical applications of **LangGraph**, a library for building stateful, multi-actor applications with LLMs.

## Table of Contents

* [smpl_langgraph.ipynb: Building a Simple Workflow](#smpl_langgraphipynb-building-a-simple-workflow)
* [Simple_chatbot.ipynb: Implementing a Simple Chatbot](#Simple_chatbotipynb-implementing-a-simple-chatbot)
* [Setup and Prerequisites](#setup-and-prerequisites)
* [Usage](#usage)

---

## smpl_langgraph.ipynb: Building a Simple Workflow

This notebook provides a foundational introduction to LangGraph by constructing a simple, branching workflow.

### Key Concepts Demonstrated:

* **State Definition:** How to define the shared graph state using `TypedDict`, in this case, a simple string `graph_info`.
* **Nodes as Functions:** Defining graph nodes as standard Python functions that receive and return updates to the graph's `State`.
    * Examples include `start_play`, `cricket`, and `football` functions.
* **Conditional Edges:** Implementing dynamic routing based on a node's output. The `random_play` function dictates the next step (either `cricket` or `football`) based on a random condition.
* **Graph Construction:** Using `StateGraph` to add nodes and define edges, including the special `START` and `END` nodes for workflow entry and exit.
* **Graph Compilation:** Compiling the graph for execution and basic structure checks.
* **Graph Visualization:** Generating a visual representation of the graph using Mermaid diagrams for better understanding of the workflow flow.

### Workflow Flow:

The graph starts at `START`, moves to `start_play`, then `random_play` makes a decision to proceed to either `cricket` or `football`, and finally, both paths converge to `END`.

---

## Simple_chatbot.ipynb: Implementing a Simple Chatbot

This notebook builds upon the basic graph concepts to implement a simple, conversational chatbot using LangGraph and integrates with Large Language Models (LLMs).

### Key Concepts Demonstrated:

* **Chatbot State Management:** Defining the `State` for a chatbot, specifically using `messages: Annotated[list, add_messages]`.
    * The `Annotated` type hint with `add_messages` reducer is crucial for correctly appending new messages to the conversation history instead of overwriting them.
* **LLM Integration:** Demonstrates how to integrate and invoke Language Models, specifically `ChatOpenAI` (e.g., `gpt-4o`) and `ChatGroq` (e.g., `qwen-qwq-32b`).
* **`mybot` Node:** A core node (`superbot` in the notebook, referred to as `mybot` in conversation) that takes the current `messages` history from the state and invokes an LLM to generate a response, which is then added back to the state.
* **Environment Variables:** Loading API keys and other sensitive information from a `.env` file.
* **Streaming Output:** Examples of streaming responses from the graph.

### Workflow Flow:

The chatbot typically starts by receiving a user message, which updates the `messages` in the state. The `mybot` node processes these messages using an LLM to generate a response, which is then added back to the `messages` list for subsequent turns.

---

## Setup and Prerequisites

To run these notebooks, you will need:

* Python 3.9+
* Jupyter Notebook or JupyterLab
* Poetry (recommended for dependency management) or `pip`

1.  **Clone the repository (if applicable):**
    ```bash
    git clone https://github.com/Abubakar0011/Langgraph_practice_simple_chatbot.git
    cd <repository_name>
    ```

2.  **Install dependencies:**

    ```bash
    # If using poetry
    poetry install

    # If using pip
    pip install langchain langgraph langchain-openai langchain-groq python-dotenv typing-extensions ipython
    ```

3.  **Set up environment variables:**
    Create a `.env` file in the root directory of your project and add your LLM API keys:
    ```
    OPENAI_API_KEY="your_openai_api_key_here"
    GROQ_API_KEY="your_groq_api_key_here"
    ```

## Usage

1.  **Start Jupyter:**
    ```bash
    jupyter notebook
    # or
    jupyter lab
    ```
2.  **Open and Run:** Navigate to `smpl_langgraph.ipynb` or `Simple_chatbot.ipynb` in the Jupyter interface and run the cells sequentially to observe the workflows in action.

---