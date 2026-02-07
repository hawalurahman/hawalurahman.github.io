---
layout: "post"
title: "I Built Local Voice Assistant"
---

I post a story on Instagram and my friends said I should talk to "someone". So I built a local voice assistant to talk to me.

It started as a joke because I post a story about going out with myself. People emphatize because it kinda look like I am alone, and they probably think I need someone to talk to. Some of my friends joked that I should just talk to AI at this point. I secretly took their advice.

So I had an idea that I want to build a local model to chat. Emphasize on the local because I don't want to use other platforms such as GPT Voice mode. I don't feel comfortable talking with their model or sharing my voice with them. Other platforms such as Gemini does not have the feature yet (because if they have I probably would've just used them instead of building one (my data is on Google anyways)). So at this point my only option is to build my own local model (probably better to call it pipeline, you'll get it later).

My wish to built the model locally, besides due to my personal preference and privacy, came with a big consequence: I have to use model small enough and light enough to run on a local machine. I don't want to stretch my machine performance too much. I would like to have a model that can run on the quietest, easiest, and lightest setup. 

So to sum it up, my requirements were:
- It has to be local
- Light enough in terms of performance

First I tried chat model with (LM Studio)[https://lmstudio.ai/]. LM Studio has a lot of options in terms of language model. This is the model that you use to generate text. I was planning to just show off some chatting interface. 

Then an idea came to my head, why don't I build the voice chat mode like the one GPT has?

So I further build the pipeline. I call it pipeline because it involves at least two different components, speech to text (to capture what I am saying) and text to speech (to say what the model are responding). So I need to have two models. In addition to these two, I also need to have one LM as a brain to generate response. 

So the pipeline would be:

my voice --> STT --> transcript --> LLM --> response --> TTS --> assitant voice

As my requirements entail, I chose the smallest model out there. Here is the list of model I use:
- (SpeechRecognition)[https://pypi.python.org/pypi/SpeechRecognition/] library for STT
- (Kokoro)[https://huggingface.co/hexgrad/Kokoro-82M#usage] for TTS
- (Gemma 3 1B)[https://huggingface.co/google/gemma-3-1b-it] for the 'brain'

I am not gonna talk about technical stuff as you can read it from my (code)[https://github.com/hawalurahman/local-assistant]

Now here is my personal review and experience on this pipeline:
- STT model works, but failed to capture punctuations. Plain text looks pretty boring to me and I am actually afraid the model would get confused. Due to my accent, model also failed to catch some phrase, especially if I speak a lil fast. But otherwise, they are doing okay given the small footprint.
- STT model (I think) have a limitation on the phrase duration, so I can't rant, I can only talk shortly. 
- STT model takes a bit of time, making it a bit unnatural if you imagine it as natural chat
- Gemma is doing okay in generating response. The issue is that I haven't turned on or configured the chat history so she would have context of what we have talked previously, so currently missing context is still very frequent (which can be an issue in a longer turn chat).
- Kokoro is genuinely good considering the size. Though the intonation is a bit unnatural and feels robotic-ish. If you aim for a natural chat, I think further fine-tuning is needed. But considering the size and parameter that they have, they are actually good, perhaps the best option out there. 

Overall, I am satisfied with the result. To me, its a learning process which have been really interesting and satisfying. I genuinely enjoy learning about text to speech model and their variants out there. With the constraint that I have, I think my pipeline performed well. 

More importantly, I get to show my friends on Instagram that I did talk to someone, though its just an AI 😂