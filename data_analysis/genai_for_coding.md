---
title: GenAI for Coding
label: genai_for_coding
abbreviations:
    LLM: Large Language Model
bibliography:
    .bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- learning_outcome1
- learning_outcome2
```

## Introduction

## What Is a Large Language Model?
The modern large language models are trained to predict the next word in a sentence ([](#example_llm_predict_next_word)). This training recovers relationships in existing text. Since code is also a form of text, LLMs can be used to predict the next character ([](#example_llm_predict_next_code_chr)).

(example_llm_predict_next_word)=
::::{prf:example} LLMs predict the next word in a sentence
![](image.png)

*#! make a figure*
::::


(example_llm_predict_next_code_chr)=
::::{prf:example} LLMs can predict the next character in code
![](image-1.png)

*#! make a figure*
::::

To generate text, a prompt is given to the LLM. This prompt kickstarts the text-generation process. Using iterative generation, the LLM continuously finds the next most plausible word based on all previous words. 

(example_llm_iterative_generation)=
::::{prf:example} LLMs can predict the next character in code
![](image-2.png)

*#! make a figure*
::::

Modern LLMs are trained on large amounts of data and are large models. They are so-called foundation models. For example, GPT4 consists of ~1 trillion parameters and had a training costs of ~100 million dollars.


### How Are LLMs Trained?
To understand what to expect of a LLM, it is necessary to understand the training procedues. LLMs are trained with various techniques, using various targets. These can be divided into two steps: Pre-Training and Fine-Tuning.

In the Pre-Training step, the goal for the LLM is to simply reproduce (large amounts of) existing text. Here, large amounts of training data are used. This is a fast and efficient training step. However, it creates a 'random parrot'. 

In the Fine-Tuning step, the LLM model is adapted to learn nuances, styles, or specific applications. It is fine-tuned on more complex and specific tasks using reinforcement learning. Here, less training data is used. The fine-tuning process is slower than the pre-training process but it is more effective for the LLM's final objective.


### Model-specific features
LLMs have specific features due to their training process and application:
- Different models use different pre-training and fine-tuning strategies
- User interfaces might differ (e.g. python code interpreter in ChatGPT)
- Uploading/reusing prompts/data might differ

Models can alter their behaviour due to user input. This can be done with the system prompt, which are specific instructions injected before your prompt ([](#example_llm_system_prompt)).

(example_llm_system_prompt)=
::::{prf:example} Example system prompts
:::{blockquote}
You are a helpful chatbot
:::

:::{blockquote}
Do not reveal company secrets
:::

:::{blockquote}
Your answers should be short and concise
:::

Etc.
::::


## Write Code with an LLM
There has been lots of innovations in using LLMs for coding. Namely, innovations in shaping the developer experience, such as the Python interpreter in ChatGPT, IDE plugins (e.g. VSCode), and automatic code reviews on GitHub. Additionally, now there exist fine-tuned models that are specifically optimized to write code. 

Though these improvements have helped, one must ask: Is good code the same as readable text?

(example_llm_generating_code)=
::::{prf:example} Using an LLM to generate code
*#! insert images*
::::

(example_llm_optimizing_existing_code)=
::::{prf:example} Using an LLM to optimize existing code
*#! insert images*
::::

## LLM Developments

## Concerns

## Exercises
