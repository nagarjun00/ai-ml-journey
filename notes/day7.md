
# Day 7 — MLPs in Transformers and How They May Store Facts

## Topics Covered

* What MLPs do inside a transformer
* How MLPs can potentially store factual associations
* Up projection, bias, activation, and down projection
* Neurons and feature detection
* Parameter count
* Superposition

## Sources

* [3Blue1Brown — MLPs in Transformers](https://www.3blue1brown.com/lessons/mlp)
* [Toy Models of Superposition](https://transformer-circuits.pub/2022/toy_model/index.html)

## Key Concept: MLPs and Facts

Attention helps tokens exchange information and build context. **MLPs provide another major part of the transformer's computation and may provide substantial capacity for storing learned associations.**

For example, when given:

`Michael Jordan plays the sport of ___`

the model may predict **basketball** because the network has learned an association between these concepts.

Research suggests that factual information is at least partly associated with MLPs, although the exact way facts are represented inside a language model is still not fully understood.

## Key Concept: How an MLP Works

An MLP processes each token's vector **independently and in parallel**. Unlike attention, the vectors don't exchange information with each other inside the MLP.

The basic structure is:

`Input → Up Projection → Activation → Down Projection → Add to Input`

The output is then added back to the original vector through the residual connection.

## Key Concept: Up Projection & Bias

The first matrix expands the token's representation into a much larger space.

You can think of each row as asking a learned question about the input:

> "Does this vector contain this particular feature?"

A **bias** is also added before the activation function.

This creates a large set of intermediate values, which can be thought of as feature detectors.

## Key Concept: ReLU / GELU & Neurons

A non-linear activation is applied to the intermediate values.

A simple example is **ReLU**:

`ReLU(x) = max(0, x)`

Negative values become zero, while positive values remain.

The values after this activation are commonly referred to as **neurons**. An activated neuron indicates that some learned feature is present strongly enough to affect the next stage.

Modern transformers often use smoother activations such as **GELU** instead of ReLU.

## Key Concept: Down Projection

The activated features are passed through another large matrix, called the **down projection**.

Its columns can be viewed as directions in the original embedding space. When a particular feature is strongly activated, its corresponding direction contributes to the output.

For our example, a feature associated with *Michael Jordan* could contribute information related to **basketball**, **Chicago Bulls**, or other learned associations.

The resulting vector is added back to the original input representation.

## Key Concept: MLP vs Attention

A useful distinction:

**Attention**

* Allows tokens to exchange information.
* Determines which other tokens are relevant.
* Uses queries, keys, and values.

**MLP**

* Processes each token independently.
* Applies learned transformations to its representation.
* Can detect and transform learned features.

So attention can help a token **gather context**, while the MLP can **process that contextualized representation**.

## Key Concept: Superposition

A tempting idea is that one neuron represents one specific fact.

In reality, this is usually too simple.

Because transformer representations exist in very high-dimensional spaces, many features can be represented using **nearly perpendicular directions**. This allows the model to represent far more features than the number of dimensions available.

This idea is called **superposition**.

As a result, one neuron may participate in representing multiple different features rather than corresponding to one clean concept.

## Key Concept: Parameter Scale

MLPs contain a huge portion of the parameters in large language models.

In the GPT-3 example discussed in the lesson, the MLP blocks account for roughly **116 billion parameters**, around two-thirds of the model's total parameters.

This helps explain why MLPs are considered an important part of the model's capacity.

## Takeaway

An MLP is essentially:

`Linear transformation → Non-linearity → Linear transformation`

The first transformation detects learned features, the activation selects which features are active, and the second transformation converts those features back into the model's embedding space.

MLPs appear to play an important role in storing and processing learned information, including factual associations. However, because of **superposition**, those facts are unlikely to be stored as simple one-neuron-per-fact representations.

## Questions I Still Have

* How exactly does training cause an MLP to learn a specific fact?
* How can we identify the features represented inside a real MLP?
* How do MLPs and attention work together across multiple transformer layers?

---

*Part of my **AI/ML learning journey** — Day 7*
