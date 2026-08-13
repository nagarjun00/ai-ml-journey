
# Day 2 — How Neural Networks Learn: Cost Functions & Gradient Descent

## Topics Covered

* Cost functions — measuring how wrong a network's output is
* Gradient descent — how a network minimizes that error
* Model comparison: Logistic Regression vs Decision Tree vs Random Forest
* Evaluation: confusion matrix, train/test split, overfitting check

## Key Concept: Cost Functions & Gradient Descent

**What makes ML different from traditional programming**
You don't write explicit instructions for the task. For digit recognition, you never write an algorithm that directly recognizes digits — instead, you write an algorithm that takes labeled example images and adjusts the network's weights and biases so it performs better on those examples.

The weights represent the strength of the connections between each neuron in one layer and the next. Each bias indicates whether its neuron tends to be active or inactive by default.

**The cost function**
We feed labeled data into the network and compare its output to the expected output (both values between 0 and 1) by squaring the difference. A correct output gives a small value; a wrong one gives a large value. Summing this across all training examples gives the cost function — a single number describing how badly the network is performing right now.

**Gradient descent**
Gradient descent is how the network finds a minimum of the cost function. The gradient is a vector pointing in the direction of steepest *increase* — so moving in the negative direction of the gradient tells us how to adjust every weight and bias to decrease the cost.

Each component of the negative gradient vector tells us two things:

* **Sign** — whether that weight/bias should be nudged up or down
* **Magnitude** — how much that change matters relative to the others

**Why this matters for training**
By repeatedly computing this gradient on labeled training data, the network incrementally moves toward a local minimum of the cost function. This iterative nudging — not any explicit rule-writing — is what "learning" means for a neural network.

## Practical Work

* Compared three models on the same dataset: `LogisticRegression`, `DecisionTreeClassifier`, `RandomForestClassifier`
* Used a proper `train_test_split` with a fixed `random_state` to check for overfitting
* Plotted a confusion matrix for the best-performing model
* Watched 3Blue1Brown's gradient descent lesson for the intuition behind `.fit()`

## Takeaway

Everything a model does when you call `.fit()` comes down to this loop: measure how wrong it is (cost function), figure out which direction reduces that wrongness (gradient), and nudge the weights that way. Understanding this made model comparison today feel less like "trying different sklearn classes" and more like watching different optimization strategies converge on the same underlying problem.

## Questions I still have

* How exactly is the gradient computed for every weight/bias simultaneously? (this is backpropagation — next video)

---

*Part of my **AI/ML learning journey** — Day 2*
