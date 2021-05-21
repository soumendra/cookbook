---
description: 'Overfitting is a spectrum, and your model lies somewhere in it.'
---

# Your network is always overfitting

## How do I think about overfitting?

Instead of thinking about only low and high training and validation loss, let's also think about the difference between training and validation loss \(generalization error\), and how it evolves over epochs. Invariably, there will be a gap between training and validation loss. Our job is to contain the overfitting. Let's look at a few ideas that we'll use to describe overfitting.

* **Model parametrization**: Given how our model is parametrized \(how many layers? how many filter/nodes per layer?\), it has certain capacity to learn. If you train it beyond its capacity to learn, it starts to memorize \(overfit\).
* **Generalization Error**: Training Loss - Validation Loss. The shape of the graph over epochs can identify regions of overfitting which may not be immidiately evident from loss graphs. The size of Generalization Error is the size of Overfitting.
* **Model/Loss Convergence**: This happens when the Loss converges to a final value \(Loss values will be around a small error range\).

## I am in a decent place. The generalization loss \(difference between training-loss and validation-loss\) has converged. What next?

Congratulations. Is the value of your `metric` satisfactory? If not, think about ways to improve your model.

## My training-loss is going down, but my validation-loss is almost static!

There could be a few reasons for this.

* Your model is over-parametrized, in which case, you need to make your model simpler/more regularised. Reduce a few layers, or reduce parameters \(kernels or nodes\) per layer, or apply dropout/L1 or L2 regularization/batch normalization.
* If your generalization loss is on a steep climb, there may be a problem with your dataset. Manually inspect it to see if the class labels have been assigned correctly. Unresolved ambiguity in class labels is the number one reason for this.

## My



