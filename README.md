# AI Helpdesk Ticket Operations Agent

An agentic application built with LangChain, Groq, and SQLite designed to simulate an enterprise ITSM operations assistant. 

## Participant Name

Mohammad Anas

## Design Patterns Implemented
* **ReAct Agent:** Uses LangGraph's prebuilt ReAct agent to enforce a strict Reason (Plan), Act (Tool Call), Observe, Reflect cycle.
* **Tool Calling:** 11 distinct SQLite tools handling searches, updates, and SLA queuing safely.
* **Archival Memory:** Uses dedicated tools to store and recall long-term user prioritization preferences.
* **Conversation Memory:** Automatically logs chat turns and includes a dedicated tool to summarize and store active sessions.
* **Safe Updates:** Uses parameterized SQL via `db_utils.py` and maintains an automatic `tool_audit_logs` record for all write operations.

## Setup
1. Create a virtual with ``uv venv`` environment and install requirements: `uv add -r requirements.txt`
2. Create a `.env` file based on `.env.example` and add your `GROQ_API_KEY`.
3. Ensure the `helpdesk_agent.db` file is placed inside the `data/` folder.
4. Run the app: `python app.py`

## Testing Prompts
Try running these sequential prompts to test the memory and update features:
1. `Show me all open high-priority tickets.`
2. `Remember that I want to prioritize Enterprise customer issues first.`
3. `Based on my preference, which tickets should I work on first today?`
4. `Summarize ticket TCK-00077.`
5. `Add a comment to TCK-00077 saying billing team is reviewing the issue.`
6. `Update TCK-00077 status to In Progress.`
7. `Summarize this conversation and store it in memory.`