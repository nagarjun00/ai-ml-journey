
# Day 4 — Backprop Calculus & Intro to LLMs/Transformers

## Topics Covered

* The calculus behind backpropagation — what the gradient vector actually contains
* How Large Language Models predict text
* Pre-training vs RLHF
* Transformers — embeddings, attention, feed-forward layers

## Sources

* [3Blue1Brown — Backpropagation Calculus](https://www.3blue1brown.com/lessons/backpropagation-calculus/#the-constituent-derivatives) / [video](https://www.youtube.com/watch?v=tIeHLnjs5U8&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=4)
* [3Blue1Brown — Large Language Models / Transformers](https://www.3blue1brown.com/lessons/mini-llm#transformers) / [video](https://www.youtube.com/watch?v=LPZh9BOjkQs&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=5)

## Key Concept: Backprop Calculus

The gradient vector we've been talking about since Day 2 isn't abstract — its entries are literally the partial derivatives of the cost function with respect to every single weight and bias in the network. Backpropagation is the algorithm that efficiently computes all of these partial derivatives, layer by layer, using the chain rule. This ties together what I learned on Day 2 (gradient descent) and Day 3 (backprop conceptually) into the actual math behind them.

## Key Concept: Large Language Models

**What an LLM actually is**
An LLM is a mathematical function that predicts what word comes next for any piece of text. Rather than predicting a single word with certainty, it assigns a probability to every possible next word.

**How it learns to predict**
Models learn by processing enormous amounts of text, typically scraped from the internet. Backpropagation is used to tweak all of the model's parameters so it becomes slightly more likely to pick the true next word and slightly less likely to pick every other word — the exact same gradient descent + backprop mechanism from Days 2-3, just applied at massive scale to a text-prediction task.

**Pre-training vs RLHF**
This process — learning to autocomplete internet text — is called pre-training, and it's only the first phase. Autocompleting random internet text is a very different goal from being a helpful assistant. To bridge that gap, models go through a second phase: Reinforcement Learning with Human Feedback (RLHF), which shapes the model's behavior toward being useful and well-behaved rather than just a good autocomplete engine.

**Why transformers changed everything**
Before transformers, most language models processed text one word at a time, sequentially. A team at Google introduced the transformer architecture, which changed this.

## Key Concept: How Transformers Work

**Step 1 — Embeddings**
The first step inside a transformer is associating each word with a long list of numbers (a vector). This is necessary because the training process only works with continuous numerical values, so language has to be encoded numerically first.

**Step 2 — Attention**
What makes transformers unique is the attention mechanism. Attention lets all of these word-vectors "communicate" with each other, refining their encoded meaning based on the surrounding context — and critically, this happens in parallel across the whole sequence, not one word at a time.

**Step 3 — Feed-forward network (MLP)**
Transformers also include a feed-forward neural network (multi-layer perceptron) step. This gives the model extra capacity to store additional patterns about language learned during training.

**Putting it together**
Data flows repeatedly through many stacked iterations of attention + feed-forward layers. With each pass, the hope is that every word's vector gets enriched with whatever information is needed to accurately predict the next word in the sequence.

## Takeaway

Everything from Days 2-4 is really one continuous idea scaling up: cost function → gradient descent → backpropagation (the mechanism) → backprop calculus (the math) → and now, LLMs, where that exact same training loop is applied to predicting text at a massive scale, on top of a transformer architecture that lets context be processed in parallel instead of word-by-word.

## Questions I still have

* How does attention mathematically decide which words to "pay attention to" — what are queries, keys, and values doing under the hood?

---

*Part of my **AI/ML learning journey** — Day 4*
