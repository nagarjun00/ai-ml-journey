# Day 1 — Neural Network Foundations: Why ReLU Beats Sigmoid

## Topics Covered

* Neural network basics (3Blue1Brown intro)
* Activation functions: Sigmoid vs ReLU
* First hands-on model: Logistic Regression (Iris / Titanic datasets, scikit-learn)

## Key Concept: ReLU vs Sigmoid

**Sigmoid's problem — saturation**
The sigmoid function squashes any input into a range between 0 and 1. Once the weighted sum going into a neuron gets very large (positive or negative), the sigmoid curve flattens out almost completely. In that flat region, the gradient (slope) is nearly zero.

**Why that matters for training**
Neural networks learn through backpropagation, which relies on gradients to know *how* to adjust each weight. If the gradient is near zero, the "signal" telling the network how to improve gets vanishingly small — this is the classic  **vanishing gradient problem** . Weights barely update, and learning stalls, especially in deeper networks where this effect compounds layer after layer.

**ReLU's advantage**
ReLU (Rectified Linear Unit) outputs the input directly if it's positive, and zero otherwise:

```
ReLU(x) = max(0, x)
```

Unlike sigmoid, ReLU's output never flattens out for large positive inputs — the gradient stays constant (1) instead of shrinking toward zero. So no matter how large the weighted sum becomes, wiggling the weights still produces a useful, non-vanishing gradient signal.

**Why this speeds up training**

* Gradients stay meaningful throughout the network, even in deep architectures with many layers.
* Weight updates remain effective instead of stalling out.
* This is a big part of why ReLU became the default activation function for deep learning — it makes training deeper networks practical and efficient.

## Practical Work

* Set up the `ai-ml-journey` repo to track this learning path
* Watched 3Blue1Brown's neural network series intro (visual intuition for weights, activations, gradients)
* Trained a first supervised model: **Logistic Regression** on the Iris and Titanic datasets using scikit-learn

## Takeaway

Activation function choice isn't just a technical detail — it directly determines whether gradients can flow properly through a deep network. ReLU's non-saturating behavior is a core reason modern deep networks are trainable at scale.

---

*Part of my **AI/ML learning journey** — Day 1*
