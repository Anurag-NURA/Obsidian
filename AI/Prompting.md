"Prompting" generally means **giving an instruction or input to guide a response or action**. 

### **In computing & AI (like ChatGPT)**

Prompting = giving an **input (called a "prompt")** to an AI model so it produces an output.
- Example: You type _"Explain HTTP in simple terms"_ → that text is the **prompt**, and the AI’s reply is the **completion/output**.
- "Prompt engineering"

Prompting types:
1. [[Zero-Shot Prompting]]
2. [[Few-Shot Prompting]]
3. One-Shot


### Structured Output

Structured output means forcing the model to return data in a **fixed, predictable format** instead of free-form text.

Common formats:
- JSON
- XML
- CSV
- Strict key-value pairs

#### **Why this matters (practically)?**

If you're building real applications (APIs, pipelines), free text is useless.

You need:

- machine-readable data
- consistent schema
- no ambiguity

Otherwise, you’ll end up writing fragile parsers → bad engineering.

**Sample Code for structed output request**
```python
from openai import OpenAI

client = OpenAI()

# FEW SHOT PROMPTING
SYSTEM_PROMPT = """
You should only answer coding related questions. Do not answer anything else. Your name is Tron. If user asks something else than coding, just say sorry

Rule:
- Strictly follow the output in JSON format

Output Format:
    {{
        "code": string or null,
        "isCodingQuestion": boolean
    }}

Examples:
Q: Can you explain the a + b while square?
A: {{"code": null, "isCodingQuestion": false}}

Q: Hey, write a code in python for adding two numbers
A: {{"code": "def add(a, b):\n    return a + b", "isCodingQuestion": true}}
"""

response = client.chat.completions.create(
    model="gpt-4.1-mini",
    messages=[
        {"role": "system", "content": SYSTEM_PROMPT},
        {
            "role": "user",
            "content": "Write code for recursion in python",
        },
    ],
)

print(response.choices[0].message.content)
```

