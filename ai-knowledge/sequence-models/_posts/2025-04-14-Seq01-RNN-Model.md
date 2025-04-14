---
layout: post
title: "Recurrent Neural Network Model"
date: 2025-04-14
categories: sequence-models
mathjax: true
tags: [sequence-models, deep-learning]
---

## Sequence Tasks in the Real World

Sequence models are designed to handle data where the order of elements matters. Here are some real-world tasks involving sequential data:

| Task                         | Input (x)                                        | Output (y)                                       |
|------------------------------|--------------------------------------------------|--------------------------------------------------|
| Speech transcription         | Audio waveform                                       | Text transcript                                  |
| Melody generation            | Short seed melody or empty input or texture prompts  | Music Snippets                        |
| Sentiment analysis           | "I didn’t enjoy the film at all."               | Negative sentiment (e.g., ★☆☆☆☆)                 |
| Genomic pattern detection    | ACTGCTAGCGTTAGCTGA                               | Highlighted segments correspond to protein                    |
| Language translation         | "Shall we go for a walk?"                      | "我们去散步好吗？"                   |
| Entity tagging               | "Yesterday, Tom met Eliza in Paris."            | Tom → Person, Eliza → Person, Paris → Location  |
| Time series forecasting      | Historical temperature readings                 | Predicted future temperature                     |

From the table above, we can see that sequence tasks fall into different categories based on input and output formats:

- **Sequence-to-sequence**: Both input and output are sequences.  
  Examples:  
  - *Speech transcription*: audio → text  
  - *Language translation*: sentence → translated sentence  
  - *Melody generation*: short prompt → music snippet  
  - *Time series forecasting*: past values → future values  
  These tasks may have input and output of different lengths.

- **Sequence-to-label**: Input is a sequence, output is a single or aligned label.  
  Examples:  
  - *Sentiment analysis*: sentence → sentiment  
  - *Genomic pattern detection*: DNA → functional region  
  - *Entity tagging*: sentence → tag sequence (same length as input)

Understanding input-output structure helps in choosing the right model (e.g., many-to-one vs many-to-many).


## Notation in Sequence Models

To work with sequence data in models like RNNs, it's important to define clear notation. Here's a typical NLP example:

**Input sequence (x):**  
*"Sherlock Holmes and John Watson lived at 221B Baker Street in London."*

We notate the sentence word by word:  
\begin{equation}
x^{<1>} = "Sherlock", x^{<2>} = "Holmes", ..., x^{<t>}, ..., x^{<9>} = "London"
\end{equation}