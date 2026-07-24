Do we have model for cyber domain?

Yes, we have.

| Model              | Purpose                                                                                                     |
| ------------------ | ----------------------------------------------------------------------------------------------------------- |
| **CyberSecEval**   | Security benchmark from OpenAI/Meta ecosystem to evaluate LLM security capabilities (not a standalone LLM). |
| **CyberLlama**     | Fine-tuned Llama models for cybersecurity tasks.                                                            |
| **SecLM**          | Security-focused language models for threat intelligence and vulnerability analysis.                        |
| **WhiteRabbitNeo** | Open-source model designed for defensive cybersecurity research and education.                              |
| **SecureBERT**     | BERT-based model for cybersecurity text classification and threat intelligence.                             |
| **CodeLlama**      | Strong at secure code analysis, vulnerability detection, and code generation.                               |
| **StarCoder**      | Useful for secure coding, code review, and vulnerability detection.                                         |


In Huggingface:

WhiteRabbitNeo series

```python
import torch
from transformers import AutoTokenizer, AutoModelForCausalLM

# ---------------------------------------------------------
# Configuration
# ---------------------------------------------------------

MODEL_NAME = "WhiteRabbitNeo/Llama-3-WhiteRabbitNeo-8B-v2.0"

SYSTEM_PROMPT = """
You are a Senior Cyber Security Analyst.

For every request:

1. Identify all vulnerabilities.
2. Mention the CWE number.
3. Mention severity.
4. Explain the attack.
5. Suggest mitigation.
6. Show secure code if applicable.

Respond professionally.
"""

# ---------------------------------------------------------
# Load Model
# ---------------------------------------------------------

print("=" * 60)
print("Loading Cyber LLM...")
print("=" * 60)

tokenizer = AutoTokenizer.from_pretrained(MODEL_NAME)

model = AutoModelForCausalLM.from_pretrained(
    MODEL_NAME,
    torch_dtype=torch.float16,
    device_map="auto"
)

print("Model Loaded Successfully\n")

# ---------------------------------------------------------
# Chat Function
# ---------------------------------------------------------

def ask_llm(user_prompt):

    messages = [
        {
            "role": "system",
            "content": SYSTEM_PROMPT
        },
        {
            "role": "user",
            "content": user_prompt
        }
    ]

    prompt = tokenizer.apply_chat_template(
        messages,
        tokenize=False,
        add_generation_prompt=True
    )

    inputs = tokenizer(
        prompt,
        return_tensors="pt"
    ).to(model.device)

    outputs = model.generate(
        **inputs,
        max_new_tokens=400,
        temperature=0.2,
        do_sample=True,
        top_p=0.95
    )

    response = tokenizer.decode(
        outputs[0][inputs["input_ids"].shape[1]:],
        skip_special_tokens=True
    )

    return response


# ---------------------------------------------------------
# Interactive Chat
# ---------------------------------------------------------

print("Cyber Security Assistant")
print("Type 'exit' to quit.\n")

while True:

    query = input("You : ")

    if query.lower() == "exit":
        break

    answer = ask_llm(query)

    print("\nAssistant:\n")
    print(answer)
    print("-" * 70)

```

NOTE: It is better to have a solid Agentic architecture compared to using Cyber-Security oriented models