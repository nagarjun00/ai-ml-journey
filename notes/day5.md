
# Day 5 — Inside GPT: Tokens, Embeddings, and Softmax

## Topics Covered

* What "GPT" actually stands for and what a transformer is
* Tokens and the embedding process
* Directions in embedding space
* Attention block vs Multilayer Perceptron (MLP) block
* Unembedding and softmax

## Sources

* [3Blue1Brown — But what is a GPT?](https://www.3blue1brown.com/lessons/gpt#unembedding) / [video](https://www.youtube.com/watch?v=wjZofJX0v4M&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=8)

## Key Concept: What GPT Means

GPT stands for **Generative Pre-Trained Transformer**. "Generative" means the model generates new text. "Pre-trained" means it was trained on huge amounts of data (same pre-training concept from Day 4). The "transformer" part is the actual architecture doing the work, and it's the main reason behind the recent boom in AI.

A transformer is a specific kind of neural network / ML model. It's not limited to text — the same underlying architecture powers voice-to-text, text-to-voice, text-to-image, machine translation, and more.

## Key Concept: The Premise of Deep Learning

Machine learning, broadly, is a body of methods where data determines a program's behavior, instead of a human explicitly encoding a set of rules. For example, to classify an image, you don't write an explicit step-by-step procedure — instead, the model has flexible parameters (like knobs and dials) that get tuned using data until the model behaves correctly. This is the same idea from Day 2's cost function and gradient descent, just framed at a higher level.

## Key Concept: Tokens & Embeddings

**Tokens**
An input is first broken into small chunks called tokens (not necessarily whole words).

**Embedding matrix**
The model has a predefined vocabulary — a fixed list of all possible tokens (e.g., ~50,000 of them). The first matrix in the transformer, the **embedding matrix**, has one column for every token in this vocabulary. This is how each token gets converted into a vector of numbers, since training only works with continuous values (same reasoning as Day 4's embeddings).

**Direction has meaning**
As the model tunes its weights during training, it settles on an embedding space where *directions* carry meaning — not just individual vector positions. Similar concepts end up pointing in similar directions in this high-dimensional space.

## Key Concept: Attention Block vs MLP Block

After the attention block (Day 4) lets word-vectors exchange context, the vectors pass through a **Multilayer Perceptron (MLP)**, also called the feed-forward layer. Unlike attention, the MLP processes each vector independently and in parallel — the vectors don't communicate with each other here; they each go through the same fixed operation.

Computationally, both the attention block and the MLP block boil down to large matrix multiplications. Understanding transformers largely comes down to understanding what these underlying matrices are doing.

After many repeated iterations of attention + MLP, all the information needed to predict the next token gets encoded into the *last* vector in the sequence. That final vector goes through one more computation to produce a probability distribution over every possible next token.

## Key Concept: Unembedding & Softmax

**Unembedding matrix**
This is essentially the reverse of the embedding matrix — it maps the model's final internal vector back into scores over the vocabulary, producing a value for every possible next token.

**Softmax**
Softmax converts an arbitrary list of numbers into a valid probability distribution — large values end up close to 1, small values end up close to 0, and everything sums to 1. It works by raising *e* to the power of each number (making everything positive), then dividing each result by the sum of all of them (normalizing so the total is 1).

## Takeaway

This ties Days 2-5 together end to end: a token gets embedded as a vector (embedding matrix) → it moves through repeated attention + MLP blocks, picking up context and pattern information (all matrix multiplications, trained via backprop from Days 2-4) → the final vector is unembedded into raw scores over the vocabulary → softmax converts those scores into an actual probability distribution the model samples the next token from.

## Questions I still have

* How does the unembedding matrix relate to (or differ from) the embedding matrix — are they ever the same weights reused (tied embeddings)?

---

*Part of my **AI/ML learning journey** — Day 5*
