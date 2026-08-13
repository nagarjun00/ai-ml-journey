
# Day 2 — Gradient Descent

**Sources:**

- 3Blue1Brown — [Gradient descent, how neural networks learn](https://www.3blue1brown.com/lessons/gradient-descent/)
- YouTube: https://www.youtube.com/watch?v=IHZwWFHWa-w&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi&index=5

## What I learned

### Cost function

What makes machine learning different from traditional programming is that you don't write explicit instructions for the task. For digit recognition, you never write an algorithm that directly recognizes digits — instead, you write an algorithm that takes in labeled example images and adjusts the network's weights and biases so it performs better on those examples.

The weights represent the strength of the connections between each neuron in one layer and each neuron in the next. Each bias indicates whether its neuron tends to be active or inactive by default.

We feed the labeled data into the network, and it produces an output. To measure how good or bad that output is, we take the difference between the expected output and the actual output (a value between 0 and 1) and square it. When the output is close to correct, this value is small. When it's wrong, the value is large. Summing this across all training examples gives the cost function — a single number describing how badly the network is performing.

### Gradient descent

Gradient descent is how we find the minimum of the cost function. The gradient of the cost function is a vector that points in the direction of steepest increase — so moving in the *negative* direction of the gradient tells us how to adjust the weights and biases to decrease the cost.

Each component of the negative gradient vector tells us two things:

- **Sign** — whether that specific weight/bias should be nudged up or down
- **Magnitude** — how much that change matters relative to the others (larger magnitude = more impactful change)

Using labeled training data lets the network repeatedly compute this gradient and move toward a local minimum of the cost function — this is what "learning" actually means for a neural network.

## Key terms

- **Cost function**: measures how wrong the network's output is compared to the expected output
- **Gradient descent**: the algorithm for finding a local minimum of the cost function by repeatedly stepping in the direction of the negative gradient
- **Local minimum**: a point where the cost is locally as low as possible — not necessarily the lowest possible cost overall
- **Weights/biases**: the adjustable parameters of the network that gradient descent tunes

## Questions I still have

- How exactly is the gradient computed for every weight/bias at once? (this is backpropagation — next video)
