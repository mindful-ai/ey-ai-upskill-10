Why does the LLM call in Langchain generation use different number of tokens in different sytems?
    - Using the same model
- | Scenario                                | Different token count? | Why                                              |
| --------------------------------------- | ---------------------- | ------------------------------------------------ |
| Same code, same model, same versions    | ❌ No                   | Prompt and tokenizer are identical.              |
| Different model version                 | ✅ Yes                  | Different tokenizers may split text differently. |
| Different `transformers` version        | ⚠️ Sometimes           | Chat templates or tokenizer behavior may change. |
| Different LangChain version             | ✅ Yes                  | Prompt construction can differ between versions. |
| Different system prompt from config/env | ✅ Yes                  | The prompt itself is different.                  |
| Different conversation history          | ✅ Yes                  | More or fewer messages are sent.                 |
| Different RAG retrieval results         | ✅ Yes                  | Different retrieved documents change the prompt. |
| Different tool definitions              | ✅ Yes                  | Agent prompts include tool descriptions.         |
