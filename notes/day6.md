
# Day 6 — Attention in Transformers

## Topics Covered

* Why attention is needed for understanding context
* Queries, keys, and attention scores
* Softmax and attention patterns
* Causal masking
* Value vectors and updating embeddings
* Multi-head attention

## Sources

* [3Blue1Brown — Attention in Transformers](https://www.3blue1brown.com/lessons/attention)
* [Video — Attention in Transformers](https://www.youtube.com/watch?v=eMlx5fFNoYc)

## Key Concept: Why Attention Is Needed

The initial embedding of a word is the same regardless of its context.

For example, **"mole"** means something different in:

* *American shrew mole*
* *One mole of carbon dioxide*
* *A skin mole*

The initial embedding doesn't know which meaning is intended. **Attention is what allows the model to update a token's representation using information from surrounding tokens.**

So, instead of thinking of a word as having one fixed meaning, attention helps create a **context-dependent representation**.

## Key Concept: Queries, Keys, and Values

A single attention head uses three learned transformations:

* **Query:** What information is this token looking for?
* **Key:** What kind of information does this token contain?
* **Value:** If this token is relevant, what information should it contribute?

For example, in *"a fluffy blue creature"*, the representation of **creature** could use its query to look for relevant information from words such as **fluffy** and **blue**.

## Key Concept: Attention Scores

The query of one token is compared with the keys of other tokens using a **dot product**.

A larger dot product means the two vectors are more aligned, so the model considers that token more relevant.

These scores form a grid showing **which tokens should pay attention to which other tokens**.

## Key Concept: Softmax & Attention Pattern

The raw attention scores are passed through **softmax**.

This converts the scores into weights between 0 and 1, with the weights for each target token adding up to 1.

The resulting values form the **attention pattern**, which determines how much information each token receives from the others.

The attention calculation is commonly written as:

`Attention(Q, K, V) = softmax(QKᵀ / √dₖ)V`

The `√dₖ` term helps keep the values at a useful scale before applying softmax.

## Key Concept: Masking

In GPT-style models, a token should not be allowed to look at tokens that come **later** in the sequence, because those tokens could reveal information about the future answer.

This is handled using **causal masking**.

Before softmax, the model effectively gives illegal future positions a score of negative infinity. After softmax, those positions receive a weight of zero.

**Masking prevents later tokens from influencing earlier tokens.**

## Key Concept: Values Update the Embeddings

The attention pattern tells the model **how much information to take** from each token.

The value transformation determines **what information is actually transferred**.

For example, if *fluffy* and *blue* receive high attention weights for *creature*, their value vectors contribute strongly to the updated representation of *creature*.

The result is a more context-aware representation, such as:

`creature → fluffy blue creature`

This process happens for every token in the sequence.

## Key Concept: Multi-Head Attention

One attention head can learn one particular type of relationship, but language contains many different relationships.

**Multi-head attention** runs many attention heads in parallel, with each head having its own learned query, key, and value transformations.

Different heads can therefore learn different patterns — grammatical relationships, word associations, long-range dependencies, and other contextual relationships.

The outputs from all heads are combined to produce the final updated representations.

## Key Concept: Attention Across the Transformer

Attention isn't a one-time operation.

Transformer blocks repeatedly apply attention and other operations such as MLPs. As the representations move deeper through the network, tokens can build increasingly rich information about their context.

This is how a token that initially represents something simple can eventually encode much more abstract information such as meaning, relationships, tone, or context.

## Takeaway

**Attention is the mechanism that lets tokens exchange contextual information.**

The basic flow is:

`Embeddings → Queries & Keys → Attention Scores → Softmax → Attention Pattern → Values → Updated Embeddings`

Queries determine **what a token is looking for**, keys determine **what other tokens offer**, and values determine **what information is transferred**.

Multiple attention heads allow the transformer to learn many different types of relationships at the same time.

## Questions I Still Have

* How exactly are the query, key, and value matrices learned during training?
* How do multiple attention heads learn different relationships instead of all learning the same thing?
* How does the attention output connect to the MLP block discussed in Day 5?

---

*Part of my **AI/ML learning journey** — Day 6*
