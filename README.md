# Langraph
2-Node Agent with Memory & Conditional Routing

A runnable, self-contained example (with fallback mock implementation)

This project demonstrates how to build a LangGraph-based agent workflow featuring:

✔️ A simple 2-node pipeline (Classifier → Retriever → Generator)

✔️ Conditional routing (retriever is skipped when not needed)

✔️ State management using TypedDict

✔️ Checkpointing / Memory using MemorySaver

✔️ Automatic fallback to a mock LangGraph when the real package is unavailable

✔️ Built-in diagnostics and unit-style tests

The project is designed so it works both inside restricted/sandboxed environments (like online judges or limited notebook runtimes) and fully supports the real LangGraph library when installed.

🚀 Features
🔹 1. Classifier → Retriever → Generator Workflow

The agent decides whether the input question needs retrieval based on simple keyword heuristics.
If required, the retriever runs; if not, we skip directly to the generator.

🔹 2. Conditional Edges

Using add_conditional_edges(), the graph dynamically chooses the next step using:

def route_after_classify(state):
    return "retriever" if state["use_retriever"] else "generator"

🔹 3. Memory / Checkpoints

The workflow includes persistent checkpoints using either:

Real langgraph.checkpoint.memory.MemorySaver, or

A mock version if the package is missing.

🔹 4. Mock LangGraph Implementation (Fallback)

If langgraph is not installed, the script auto-loads a built-in mini framework that mimics:

StateGraph

MemorySaver

Graph compilation

Node routing

.invoke() execution flow

This ensures your example always runs, even in restricted environments.

🔹 5. Diagnostics & Debug Printouts

Before compiling the graph, the script prints:

Registered nodes

Registered edges

Any potential invalid transitions

Helpful for debugging compilation issues.

🔹 6. Built-in Unit Tests

The script includes lightweight tests:

Factual question → must use retriever

Opinion question → must skip retriever

“What is” question → must trigger retriever

All tests run automatically when executing.
