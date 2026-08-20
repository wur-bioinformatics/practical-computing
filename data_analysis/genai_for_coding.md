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

### Model-specific features

## Write Code with an LLM

## LLM Developments

## Concerns

## Exercises
