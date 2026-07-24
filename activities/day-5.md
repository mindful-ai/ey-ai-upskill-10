### 5.1 Langgraph [10]

- Run the examples 
- Ref: 23-langgraph-orchestration

--------------------------------------------------
11:10 - 11:30 Tea Break
11:30 - 11:40 Exercise 5.1 [+5]
--------------------------------------------------


### 5.2 Langsmith 

#### Phase 1 [10]

- Run 24-langsmith-observability\db-graph-buggy-code.py 
  - Observe that it stuck
  - Press CRTL+C to exit
- Update 24-langsmith-observability\01-db-graph-buggy-code-tracing.py
  - Copy from https://github.com/mindful-ai/ey-ai-upskill-10/blob/main/24-langsmith-observability/01-db-graph-buggy-code-tracing.py
- Connect to smit.langchain.com
  - Sign-up and create the API keys
  - Store in the key-vault

--------------------------------------------------
12:10 - 12:20 5.2.1
--------------------------------------------------

#### Phase 2 [15]

- Observe how langsmith @traceable decorator is used
- Run the code and observe the trace in langsmith web interface
- Notice 3 red flags:
  - Tool error
  - max retries stuck at 1
  - Retry always back to planner
- Understand the fix for router
  - Notice that state["retries"] is mutated in local scope
    - This does not take effect
  - Use return {"retries": state["retries"]}
- Add code to handle Tool Error
  - Uncomment the sections of the code in executor, validator and router
  - Re-run the code and observe all queries complete execution

--------------------------------------------------
12:55 - 1:10 5.2.2
--------------------------------------------------

--------------------------------------------------
1:40 - 2:40 Lunch Break
--------------------------------------------------

### 5.3 Capstone Project Execution [180]

#### Phase 1: Setting up CIS RAG tool

- Ref: 16-rag-capstone\cis-basic\README.md
- Execute python commands as specified and test the RAG
- Understand the RAG architecture in this project
- Create api.py using ChatGPT to expose the functionality as an end-point
  - Use FastAPI
  - Use curl command to test it

--------------------------------------------------
4:15 - 4:35 Tea Break
--------------------------------------------------
