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

We notate (tokenize) the sentence word by word:  
$$
x^{\langle 1 \rangle} = \text{"Sherlock"},\quad x^{\langle 2 \rangle} = \text{"Holmes"},\quad \dots,\quad x^{\langle t \rangle},\quad \dots,\quad x^{\langle 12 \rangle} = \text{"London"}
$$

We use \\(T_x = 12\\) to denote the length of the input sequence.  

**Output sequence (y):**  
Suppose the task is **named entity recognition (NER)**, where each word gets a binary label:  
$$
y^{\langle 1 \rangle} = 1, y^{\langle 2 \rangle} = 1, \quad \dots, \quad y^{\langle t \rangle},\quad \dots,\quad y^{\langle 12 \rangle} = 0
$$

Here the label \\(y = 1\\) means the corresponding word is a part of a name, while \\(y = 0\\) means the corresponding word is **not** a part of a name. The output length \\(T_y = 12\\) in this case is the same as \\(T_x\\), because we're predicting one label per token. But in general, \\(T_x\\) and \\(T_y\\) could be different for other tasks.  

For the **i-th** training example:
  - Here, one example represents one sentence. The whole dataset may contain a lot of sentences.
  - \\(X^{(i)\langle t \rangle}\\): the **t-th** word in the **i-th** sentence (example) in the dataset.
  - \\(Y^{(i)\langle t \rangle}\\): the **t-th** label in the **i-th** sentence (example) in the dataset.
  - \\(T_x^{(t)}\\), \\(T_y^{(t)}\\): input/output lengths for example **i**.


## Representing Words: One-Hot Encoding

To process natural language with sequence models, we first need to convert words into numerical representations. We do it through two steps.  

1. **Vocabulary construction**

    | Index  | Word        |
    |--------|-------------|
    | 1      | a           |
    | 2      | aaron       |
    | ...    | ...         |
    | 367    | at          |
    | ...    | ...         |
    | 4076   | Holmes      |
    | ...    | ...         |
    | 7235   | Watson      |
    | ...    | ...         |
    | ...    | ...         |
    | 10,000 | `<UNK>`     |

    > Note: Words not in the vocabulary are mapped to `<UNK>` (unknown token).

  Assume vocabulary size \\( |V| = 10000 \\).

2. **One-hot encoding**

    Each word \\( x^{\langle t \rangle} \\) is represented as a one-hot vector of **length 10,000**:
    - A vector with all zeros except a 1 at the index corresponding to the word
    - For example:  
        - "Holmes" → a vector with 1 at position 4076, 0s elsewhere  
          $$
          x^{\langle 2 \rangle} = \text{one-hot}("Holmes") =
          [0,\, 0,\, \dots,\, 0,\, \underset{4076}{1},\, 0,\, \dots,\, 0] \in \mathbb{R}^{10000}
          $$
        - "Watson" → 1 at position 7235, 0s elsewhere  
          $$
          x^{\langle 5 \rangle} = \text{one-hot}("Watson") =
          [0,\, 0,\, \dots,\, 0,\, \underset{7235}{1},\, 0,\, \dots,\, 0] \in \mathbb{R}^{10000}
          $$
        - "221B" → 1 at position 10000, 0s elsewhere ("221B" is not in our vocabulary, so it is mapped to `<UNK>`)
          $$
          x^{\langle 8 \rangle} = \text{one-hot}("221B") =
          [0,\, 0,\, \dots,\, \underset{10000}{1}] \in \mathbb{R}^{10000}
          $$

    🔍 One-hot encoding is simple and works well for small vocabularies, but:  
      - It does **not capture semantic similarity** (e.g., "cat" and "dog" are equally distant as "cat" and "carpet").  
      - The vectors are **sparse** and **high-dimensional**.  

    Later we'll explore more expressive word representations like **word embeddings** (e.g., word2vec, GloVe).

    Thus, an entire sentence can be represented as a sequence of one-hot vectors, typically organized into a 2D array (matrix) of shape \\( T \times V \\), where \\( T \\) is the number of tokens in the sentence and \\( V \\) is the vocabulary size. Our task is to find a map \\(f\\) to map from the input \\(x\\) to the target \\(y\\).
