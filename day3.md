
# Day 3 — Backpropagation: How a Network Assigns Blame

## Topics Covered

* Backpropagation — how a single training example nudges weights, biases, and activations
* Why the same input can give different results depending on features not seen in training
* Mini-batches and Stochastic Gradient Descent (SGD)

## Key Concept: Backpropagation

**Three ways to reduce cost for one training example**
For any given output neuron, there are three levers that can move its activation toward the correct value:

1. Increase/decrease the **bias**
2. Increase/decrease the **weights** feeding into it
3. Change the **activations** of the previous layer feeding into it

**Why a trained network can still get things wrong**
A network's performance is only as good as what it saw during training. If a factor like size, color, or perspective wasn't represented in the training data, the network has no learned basis for handling it correctly — so it can produce unexpected results on inputs that vary along those unseen dimensions.

**Nudging weights and biases correctly**
To push the output toward the correct answer, we want to nudge the weights connected to the *most active* neurons the most — since those connections have the biggest influence on the output. For example, to make a network output "2" instead of the wrong answer, we'd increase the bias/weights associated with the "2" neuron and decrease those associated with all other output neurons.

The neurons producing a stronger (brighter) activation are the ones most responsible for the current output — so they matter most when deciding where to make changes.

**How weight changes propagate**
The effect of increasing a weight is proportional to the activation it's multiplied by — a weight connected to a highly active neuron will move the output more than the same size change on a weight connected to a barely-active neuron. In other words, the change in an activation (aᵢ) is proportional to its corresponding weight (wᵢ).

**Propagating backward through layers**
Once we know what change is wanted for one layer's activations, backpropagation lets us work backward — the desired activations become the target for the previous layer, and we repeat the same process: figure out which weights/biases in that layer to adjust. Doing this layer by layer, back through the whole network, is what "backpropagation" refers to.

**From single example to batches**
Computing the ideal weight/bias nudge for every single training example individually, then averaging across the entire dataset, would be accurate but far too slow. So instead, the training data is split into **batches**, and further into **mini-batches**. Gradient descent is run on each mini-batch instead of the full dataset — this is called **Stochastic Gradient Descent (SGD)**. It's less precise per step than using the full dataset, but the speed gain makes it far more practical, and it still converges toward a good minimum over many steps.

## Takeaway

Backpropagation is really just gradient descent applied layer by layer, working backward from the output: figure out what change each neuron's activation "wants," then trace that want back through its weights and biases, and repeat for the previous layer. Doing this per mini-batch (SGD) instead of the full dataset is what makes training deep networks computationally feasible.

## Questions I still have

* How exactly is the chain rule applied mathematically to propagate the gradient backward layer by layer?

---

*Part of my **AI/ML learning journey** — Day 3*
