---
layout: post
title: Interacting with Large Language Models and Transformers
---

Here are several codes that I often use to interact with Large Language Models (LLMs) and Transformers so I don't have to reopen my old jupyter notebooks and Hugging Face documentation:

## Login

You need to login when you want to access gated repositories such as Llama and Mistral. 

```python
from huggingface_hub import login

login(token="insert_your_token")
```

## Load pipeline

Pipeline is simpler to interact since we do not have to think or maintain how tokenizer and model interact. However, you have to make sure that the model supports the use. Usually LLMs have it but smaller Transformers might not. Fine-tuned models might have it.

### big boi LLMs

```python
import transformers
import torch

model_id = "meta-llama/Meta-Llama-3.1-8B-Instruct"

pipe = transformers.pipeline(
    "text-generation",
    model=model_id,
    model_kwargs={"torch_dtype": torch.bfloat16},
    device_map="auto",
)
```

notes:
- device map auto helps when you have multiple gpus.
- torch dtype helps reduce memory use (fp32 is highest, work your way down)
- "text-generation" is called the task. Often pipeline used "text2text-generation"

### smaller fine dudes

```python
from transformers import pipeline

pipe = pipeline("text2text-generation", model="hawalurahman/idt5-base-qaqg-extend")
```

### when pipeline does not work

Yepp, this is the manual way. See the difference? Pipeline handles everything from inputs to decoding the output from Transformers. 

```python
from transformers import AutoTokenizer, AutoModelForSeq2SeqLM

tokenizer = AutoTokenizer.from_pretrained("hawalurahman/idt5-base-qaqg-extend")
model = AutoModelForSeq2SeqLM.from_pretrained("hawalurahman/idt5-base-qaqg-extend")

text = f"here_is_your_prompt"
inputs = tokenizer(text, return_tensors="pt").input_ids.to('cuda')
outputs = model.generate(inputs, max_new_tokens = 200)
outputs_txt = tokenizer.decode(outputs[0], skip_special_tokens=True)
```
notes:
- AutoModelForSeq2SeqLM needs to be adjusted based on the model architecture and use case
- max_new_tokens can be adjusted
- this code is used for cuda devices, if not, just remove the to('cuda') -- smaller transformers models do not require cuda

## Prompting

I like to use prompting provided with pipeline. 

```python
prompt1 = [
    {"role": "user", 
    "content": "write_the_prompt_here"}
]

response = pipe(prompt1)
```

You can also wrap it in a function if you have more context. We wrap additional context via f-string. 

```python
def prompt1(context1, context2):
    prompt = [
        {"role": "user", 
        "content": f"write_the_prompt_here given {context1} and {context2}"}
    ]
    return prompt

response = pipe(prompt1(name, address))
```

## Conclusion

yep thats pretty much what I often used. Might update it later lads!

Cheers,

Halim