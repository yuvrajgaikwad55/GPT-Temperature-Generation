
from transformers import pipeline
import torch

generator = pipeline(
    "text-generation",
    model="distilgpt2",
    device=0 if torch.cuda.is_available() else -1
)

prompt = "Explain Artificial Intelligence in about 50 words."

temperatures = [
    0.1, 0.2, 0.3, 
]

for temp in temperatures:
    print("=" * 70)
    print(f"Temperature = {temp}")

    output = generator(
        prompt,
        max_new_tokens=40,
        temperature=temp,
        do_sample=True,
        top_p=0.95,
        top_k=50,
        pad_token_id=generator.tokenizer.eos_token_id
    )

    print(output[0]["generated_text"])
    print()
