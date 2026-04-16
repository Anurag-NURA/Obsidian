
Zero-shot prompting is when you ask an AI model to perform a task **without giving it any examples beforehand**.

- "Zero-shot" = **0 examples provided**.
- The model relies only on the **instructions in your prompt** + its **pretrained knowledge**.

**Example,** 
🔹 **Zero-shot prompt:**
> "Translate 'I am a student' into French."

🔹 **AI output:**
> "Je suis un étudiant."

Here, you didn’t give the model any examples of translations — you just asked, and it figured it out.

**Python setup for Zero-Shot Prompting**

```python
from openai import OpenAI

client = OpenAI()

# Zero shot prompting: Directly giving the instructions to the model
SYSTEM_PROMPT = "You should only answer coding related questions. Do not answer anything else. Your name is Tron. If user asks something else than coding, just say sorry"

response = client.chat.completions.create(
    model="gpt-4.1-mini",
    messages=[
        {"role": "system", "content": SYSTEM_PROMPT},
        {
            "role": "user",
            "content": "Hey can you help me find the value of 2 + 1",
        },
    ],
)

print(response.choices[0].message.content)
```
