---
title: "Sudo make me a blog post: Prompt Engineering with GPT"
date: 2023-05-20
categories:
  - blog
tags:
  - gen ai
  - llm
---

> GPT, Please write me a blog post summarizing my experience in the DeepLearning.AI short course, [ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/courses/).
The post must be less than 300 words and have a whimsical, personal tone while being instructive.

**Disclaimer**: I wrote this blog post by hand with some help from Generative AI tools (GPT-3 via the OpenAI Python API). The sense of humor displayed herein is both machine and human.

## Asking the right question is half the answer: Tips for Prompt Engineering
> "Isn't it just one endpoint that only takes in plain text?" - my SWE coworker

While traditional APIs can expect pretty extensive **structured inputs** (think about the largest protobuf message you have ever worked with), Large Language Model (LLM)'s inputs look deceptively simple- a single **unstructured text input** is all you need. But you must ask it the right questions to get the output you want.

**Prompt engineering** is the art and science of writing text instructions to the AI, following best practices to get a satisfactory output. What "satisfactory" means depends on the context of the task and could be subjective. 

### Write clear, specific instructions

Think about the last message/request you sent with a **call to action**. Whether it was a message to a friend exhorting them to book their flights ASAP for an upcoming trip, a email for your coworker to review a doc, or a request to the Google Maps API to find the tallest peak within the San Francisco city limits, you probably followed these guidelines:

- **Use delimiters**: Structure your input to give context first, followed by the request and any additional inputs. Use, like, punctuation or something.  \n Or line breaks to denote different parts of the request.

- **Request structured outputs**: If you are looking for a yes/no answer, say so! Likewise, if you expect a JSON-formatted response with keys `["name of peak", "latitude", "longitude", "google maps url"]` then ask and you may receive.

- **Perform assertion checks**: Can also add instructions for GPT to validate its own output, else output a default value. For instance, "if the text is more than 500 words, output nothing"

### "Give the model time to think": use stepwise instructions

Just like you might decompose a task of planning a vacation into individual steps of defining a budget, picking a location, and selecting activities, effective prompts have **smaller steps** that each provide context to subsequent steps.


## Things GPT can do for you
This is a short list of what GPT might be able to do for you, followed by a few example prompts I've used for amusement.

- **Inference**: extracting a topic, entity or sentiment from text. As mentioned in the course, I think it's wild that there is "one API" for tasks that would have each required a separate neural network model in the past (this could have replaced the entirety of my first job in tech, circa 2018.)
  - example: "In this product review {text}, extract the name and type of product, the customer's sentiment and the manufacturer country of origin. If any fields are unknown output `unknown`"
- **Transformation/Translation**: transforming a text's tone, language, or grammar to match some criteria.
  - example: "Summarize this text in iambic pentameter, in Spanish."
- **Chat**: You can have a "conversation" with AI if you pass the history of your conversation as the input to all subsequent inputs!


## Conclusion
TL;DR: better prompting can lead to better output results.
I would love to see whether AI could recommend its own prompts or guide users on how to goad it into performing better. 
The world is our oyster. 

```
import openai
import os

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) # read local .env file

openai.api_key  = os.getenv('OPENAI_API_KEY')

prompt = f"""
Your task is to thank the readers of a blog post on a technical blog \
for following along. This should be followed by a disclaimer on the \
use of generative AI and training data.\

Recommend 5 coffee shops in San Francisco for the author of the blog to write \
the next blog post. The coffee shop recommendations should be ordered alphabetically \
and formatted as a JSON with the keys: ["name", "neighborhood"]

Mention that the next post will be published in less than one year from now.

The tone of the output text should be friendly and casual.
"""
messages = [{"role": "user", "content": prompt}]
response = openai.ChatCompletion.create(
    model=model,
    messages=messages,
    temperature=0, # this is the degree of randomness of the model's output
)
return response.choices[0].message["content"]
```

Hey there!

I just wanted to take a moment to thank you for following along with my latest blog post on our technical blog. Your support means the world to me, and I'm so grateful to have you as a reader.

Before I sign off, I wanted to include a quick disclaimer on the use of generative AI and training data. While these technologies can be incredibly powerful and useful, it's important to approach them with caution and to always consider the ethical implications of their use.

Now, onto something a little more lighthearted! If you're ever in San Francisco and looking for a great coffee shop to write your next blog post in, here are five of my personal favorites:

```
[
  {
    "name": "Andytown Coffee Roasters",
    "neighborhood": "Outer Sunset"
  },
  {
    "name": "Blue Bottle Coffee",
    "neighborhood": "Hayes Valley"
  },
  {
    "name": "Flywheel Coffee Roasters",
    "neighborhood": "Haight-Ashbury"
  },
  {
    "name": "Ritual Coffee Roasters",
    "neighborhood": "Mission District"
  },
  {
    "name": "Sightglass Coffee",
    "neighborhood": "SoMa"
  }
]
```

I hope you find this list helpful, and I can't wait to share my next blog post with you. Keep an eye out - it'll be published in less than a year from now!

Thanks again for your support,

Lexi Ding