
## 1. N-grams (Bigrams & Trigrams)

### What is an n-gram?
An **n-gram** is a contiguous sequence of `n` tokens (words or characters) from text.

- Unigram: 1 word
- Bigram: 2 consecutive words
- Trigram: 3 consecutive words

Example sentence:
> the cat sat

- Bigrams: (the, cat), (cat, sat)
- Trigrams: (the, cat, sat)

### What n-grams are used for
- Language modeling
- Next-word prediction
- Estimating probabilities from counts

### Probability intuition
Bigram model:
P(w_t | w_{t-1})

Trigram model:
P(w_t | w_{t-2}, w_{t-1})

### Limitations
- Cannot generalize to unseen sequences
- Vocabulary explosion
- No semantic understanding
- Fixed context window

---

## 2. Word Embeddings (High-Level)

### What is a word embedding?
A **word embedding** maps a word to a dense numeric vector:

word → R^d

Example:
"cat" → [0.12, -0.45, 0.88, ...]

### Why embeddings matter
- Capture semantic similarity
- Reduce dimensionality vs one-hot vectors
- Enable generalization

Key idea:
> Distance in embedding space ≈ semantic similarity

---

## 3. Word2Vec (High-Level)

### What Word2Vec is
**Word2Vec** is a method for learning word embeddings from context.

Words appearing in similar contexts learn similar vectors.

### Two main variants
- CBOW (Continuous Bag of Words): predicts a word from its context
- Skip-gram: predicts context words from a center word

### Why Word2Vec was important
- Learned embeddings automatically
- Captured analogies (king − man + woman ≈ queen)
- Foundation for modern NLP models

---

## 4. Embeddings in Modern Models

### How embeddings are used
1. Word → embedding lookup
2. Embedding passed to a model (RNN, Transformer)
3. Model operates on vectors, not raw words

### Key properties
- Learned during training
- Task-dependent
- Shared across the model

---

## 5. Recurrent Neural Networks (RNNs)

### What problem RNNs solve
RNNs model **sequences**, where order matters:
- Language
- Time series
- Audio
- Logs

They do this by maintaining state (memory).

---

## 6. Core RNN Idea: Hidden State

At each timestep t, the RNN maintains a hidden state:

h_t = current memory of the sequence

The hidden state:
- Encodes information from previous inputs
- Is passed forward through time
- Is reused at every timestep

---

## 7. RNN Computation (Core Equation)

### Pre-activation
z_t = W_x x_t + W_h h_{t-1} + b

### Activation
h_t = tanh(z_t)

### Variable meanings

| Symbol | Meaning |
|------|--------|
| x_t | Input vector at time t |
| h_{t-1} | Previous hidden state |
| W_x | Input-to-hidden weight matrix |
| W_h | Hidden-to-hidden weight matrix |
| b | Bias vector |
| h_t | Updated hidden state |

---

## 8. What the Hidden State Represents
- Compresses prior inputs into a fixed-size vector
- Acts as the model’s memory
- Influences future predictions

---

## 9. Output Layer (High-Level)
Often:
y_t = softmax(W_y h_t + b_y)

Used for:
- Next-word prediction
- Sequence labeling
- Classification per timestep

---

## 10. Vanishing Gradient Problem

### What it is
During backpropagation through time:
- Gradients are multiplied repeatedly across timesteps
- With tanh, gradients shrink

### Why this is a problem
- Early timesteps receive little learning signal
- Long-range dependencies are hard to learn

### Consequence
Led to architectures like LSTM and GRU.

---

## 11. Big Picture Comparison

| Concept | What it Captures |
|------|----------------|
| Bigrams / Trigrams | Local word patterns |
| Word2Vec | Semantic similarity |
| Embeddings | Dense word meaning |
| RNNs | Sequential dependencies |
| Hidden state | Memory over time |

---

## 12. One-Sentence Summary
N-grams model local patterns, embeddings capture meaning, and RNNs process sequences using hidden states, but struggle with vanishing gradients on long sequences.
