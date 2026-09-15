# What I Learned

## Avoiding Overfitting

data normalization

step size, iter amount

Divide by zero error in log loss: Caused by initializing slope and bias like linear regression (way too big, caused sigmoid to saturate early).
Fixed by initializing it between 0 and 1. However, the same error continued to occur, solved by clipping the probs array so that no values so small that the 
program interprets them as 0 or 1 are passed into log, which would cause the program to break.

## Step Size
Started way too high, caused loss to oscillate back and forth instead of converge

## Iter Amount
Was way too low, increased from 20 to 1000

## Features Didn't Line Up
Study time didn't really have a good correlation with if students got a B or higher. Changed x to "final_exam_score", which went much better.

## Normalizing The X Features
The gradient of the loss wrt. the slope = dlds = (probs - y) * x,

Meanwhile:

The gradient of the loss wrt. the bias = dldb = (probs - y) * 1.

In this analysis, x can range from 45 to 100, making the gradient of the slope far greater than the gradient of the bias.
Because the same step size is applied to the slope and bias, the slope will move far more than the bias per step.

To ensure this doesn't happen, we can apply z-score normalization to the xs, which rescales it to roughly [-2, 2] with a mean of 0.
This allowed both gradients to move at a similar pace, making accurate gradient descent possible.
Additionally, by keeping the xs small we can squish it through sigmoid better.

### Ensuring The Test Set Was Normalized With The Training Set's Coordinate System
We needed to ensure that the test set's xs were all matched to the training set's coordinate system so that `probs` would fit to it,
Because `probs` was made using the training set's coordinate system.