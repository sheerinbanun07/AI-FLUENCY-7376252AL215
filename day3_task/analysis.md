# Agentic AI: Foundations and Open-Source Practice

## Scenario

The scenario used in this project is a college course fee checker. An external `notice.txt` file contains the fees for two courses, CS101 and AI202, along with a 20% Merit Scholarship rule.

## Key Concepts

### LLM

A Large Language Model (LLM) is an AI model that understands and generates natural language. A plain LLM answers questions using the information available in its model context, but it cannot automatically access a local file unless a tool or other external mechanism is provided.

### Agent

An agent is an LLM-based system that can decide what action to take to complete a task. When necessary, it can use tools, receive their results, and continue reasoning to produce a final answer.

### Tool

A tool is an external function that gives the LLM access to information or capabilities that it does not have directly. In this project, the tool is `read_notice()`, which reads the contents of `notice.txt`.

### Tool Call

A tool call is the LLM's request to execute a particular tool. In this project, the model requested the `read_notice` tool when it needed the actual course fee information.

### Tool Schema

A tool schema describes a tool to the LLM. It includes the tool name, description, and parameters. The schema used in this project tells the model that `read_notice` reads the college fee notice and requires no arguments.

### Tool-Call Flow

The flow used in this project is:

User question -> LLM -> Tool call -> Tool execution -> Tool result -> LLM -> Final answer

For the fee question, the LLM requested `read_notice`. The tool returned the contents of `notice.txt`, and the LLM used that information to calculate the fees after the scholarship.

### Why Tool Results Are Plain Text

A tool returns its result as data that the LLM can process. Plain text is simple, flexible, and easy for the model to interpret. If a tool fails, it can also return an error message as text, allowing the LLM to understand that the requested action did not succeed and respond appropriately.

## Plain LLM vs LLM With One Tool

| Aspect | Plain LLM | LLM with One Tool |
|---|---|---|
| General knowledge | Yes | Yes |
| Access to external notice | No | Yes |
| Can call a function | No | Yes |
| Can use tool results | No | Yes |
| Can calculate using information provided in the question | Yes | Yes |
| Can retrieve missing local information | No | Yes |

## Implementation

The project contains three Python files:

- `no_tool.py` demonstrates a plain LLM without external tools.
- `tool.py` contains the `read_notice()` tool.
- `tool_agent.py` demonstrates an LLM connected to the `read_notice` tool.

The `notice.txt` file provides the external college fee information.

## Observations

### Question 1

**Question:** What are the fees for CS101 and AI202 after the 20% merit scholarship?

**Result:** The model called the `read_notice` tool. The tool returned the course fees and scholarship information. The final answer calculated CS101 as INR 40,000 and AI202 as INR 48,000.

**Observation:** A tool was required because the exact fee information was stored in the external notice.

### Question 2

**Question:** What is a merit scholarship?

**Result:** The model did not call the tool and answered using general knowledge.

**Observation:** The external college notice was not necessary for this general question.

### Question 3

**Question:** If the CS101 fee is INR 50,000 and the scholarship is 20%, what is the final fee?

**Result:** The model did not call the tool and calculated the answer as INR 40,000.

**Observation:** The required numbers were already provided in the question, so the external notice was unnecessary.

## Suitability and Conclusion

A plain LLM is suitable for general questions and calculations when all required information is already available in the prompt. However, it cannot reliably answer questions that require information stored in an external source that it cannot access.

An LLM with a tool is suitable when the task requires external or local information. In this scenario, the tool allowed the model to retrieve the college fee notice and then use that information to produce the final answer.

This experiment demonstrates that an agent does not need to call a tool for every question. The LLM can decide whether a tool is necessary based on the information required to answer the question.