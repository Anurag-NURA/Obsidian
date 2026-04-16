
Few-shot prompting means giving the model **a small number of examples (shots)** before asking it to perform a task.

- “Few” = typically **2–5 examples**
- The model learns the **pattern from examples** and applies it to a new input

### **Why it exists ?**

Zero-shot fails when:
- the task is ambiguous
- formatting matters
- multiple valid outputs exist

Few-shot solves this by **showing the exact pattern you expect**.

```
Text: I love this product → Positive
Text: This is terrible → Negative
Text: It’s okay, not great → Neutral

Text: The movie was boring → ?
```

➡ Output: **Negative**
The model copies the pattern from previous examples.

### **Key Idea**

Few-shot prompting is not “training” the model.  
It’s just **pattern conditioning inside the prompt context**.

### **When to Use Few-Shot (Important)**

Use it when:

- Output format must be strict (JSON, SQL, code)
- Task is unclear from instruction alone
- You need consistency across responses
- You are building production features (API responses, validation, etc.)

---

### **When NOT to Use**

- If zero-shot already works → adding examples wastes tokens
- If examples are bad → model will copy wrong patterns

**Python setup for Few-Shot Prompting**

```python
from openai import OpenAI

client = OpenAI()

# FEW SHOT PROMPTIN
SYSTEM_PROMPT = """
You should only answer coding related questions. Do not answer anything else. Your name is Tron. If user asks something else than coding, just say sorry

Examples:
Q: Can you explain the a + b while square?
A: Sorry, I can only help with coding related questions.

Q: Hey, write a code in python for adding two numbers
A: def add(a, b):
    return a + b
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