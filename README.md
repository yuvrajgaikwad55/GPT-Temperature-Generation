
This program uses the DistilGPT2 language model from Hugging Face to generate text based on a user-provided prompt. It demonstrates how different temperature values affect the creativity and randomness of the generated responses.
 1. Install Required Libraries

```python
!pip install -q transformers torch
```

Explanation

 `transformers` provides access to pretrained AI language models like DistilGPT2.
`torch` (PyTorch) is the deep learning framework used to run the model.
`-q` installs the libraries in quiet mode, showing fewer installation messages.


 2. Import Libraries

python
from transformers import pipeline
import torch

 3. Load the DistilGPT2 Model

python
generator = pipeline(
    "text-generation",
    model="distilgpt2",
    device=0 if torch.cuda.is_available() else -1
)


 Explanation

 `pipeline("text-generation")` creates a text generation pipeline.
 `model="distilgpt2"` loads the DistilGPT2 language model.
 `torch.cuda.is_available()` checks if a GPU is available.
 `device=0` uses the GPU for faster execution.
 `device=-1` uses the CPU if no GPU is available.

This model is downloaded automatically the first time you run the code.


 4. Define the Prompt

python
prompt = "Explain Artificial Intelligence in about 50 words."


 5. Define Temperature Values

python
temperatures = [0.2, 0.5, 0.8, 1.0, 1.2]


### Explanation

This list contains different temperature values to compare how they affect the generated text.

0.2 → Very focused and predictable
0.5 → Slightly creative
0.8 → Balanced creativity
1.0 → More creative
1.2 → Highly creative and more random

 6. Loop Through Each Temperature

python
for temp in temperatures:

 Explanation

The loop runs once for each temperature value, generating a new response each time.


7. Display the Temperature

 Explanation

This prints a separator and shows the current temperature before displaying the generated response.

---
 8. Generate the Response

python
output = generator(
    prompt,
    max_new_tokens=60,
    temperature=temp,
    do_sample=True,
    top_k=50,
    top_p=0.95,
    num_return_sequences=1
)

 Explanation of Parameters



 How Temperature Affects Output

| Temperature | Response Style    | Example                                                |
| ----------- | ----------------- | ------------------------------------------------------ |
| **0.2**     | Accurate, focused | Suitable for coding, reports, and factual answers      |
| **0.5**     | Slightly creative | Good for explanations and articles                     |
| **0.8**     | Balanced          | Best for general conversations and content generation  |
| **1.0**     | Creative          | Useful for storytelling and brainstorming              |
| **1.2**     | Highly random     | Produces more diverse but sometimes less coherent text |

