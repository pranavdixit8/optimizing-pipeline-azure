# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary

In this project, we build a classifier to predict if the customer of the bank will subscribe to a term deposit with the bank or not. We explore and compare the HyperDrive option of finding the best hyperparameters for logistic regression using the Sklearn library, with the AutoML option which explores different types of classifaction models and hyperparameters.

With the limitation of using interactive authentication, we have explored the option of just 4 runs to find the best hyperparameters using HyperDrive. The best performance with the HyperDrive option is the accuracy of 91.20 %. Similarly, we have just used 4 interations of AutoML options so that we can compare the two options. With AutoML the best performance results in accuracy of 91.77 % with the model: VotingEnsemble.


## Scikit-learn Pipeline

In the Sklearn pipeline, we use Logistic Regression model for classification with tuning the hyperparameters using Hyperdrive. The hyperparameters used are: C (Inverse of regularization factor) and max_iter(maximum number of iteration). For the purpose of tuning the hyperparamters, we have used the primary metric as "Accuracy" with goal of maximizing it.

We have used random sampling, allowing us to do initial search to understand the affects of different parameters on the algorithm. It allows us to refine the search space to improve results.

We have multiple options for early termination policy, for our runs we have used Bandit policy. The policy terminates runs where the primary metric is not within the slack factor compared to the best performing run. This helps in ignoring runs which we know won't result in the best run, resulting in saving time and resources for the experiment. Care should be taken to choose a proper slack factor while using Bandit policy.


## AutoML

In the AutoML option, we have used the task as "clasification" and primary metric as "accuracy" and iterations as 4, so that we can compare this option with the HyperDrive option. The best run with AutoML was given by the model: VotingEnsemble with accuracy of 91.77%.

## Pipeline comparison

In our experiments, the performance of 2 options is comparable, with HyperDrive option having an accuracy of 91.20 % while AutoML option having accuracy of 91.77 %. Even with consideration to the limitation of our experiments and limited data points, we can say that AutoML will result in a better performance as AutoML go through multiple classifciation models while the HyperDrive option just uses the Logistic Regression Algorithm.

## Future work

We can use Service principal to automate the authentication, allowing us to do considerably higher number of iteration. With HyperDrive, once we have done an intial search using Random Sampling, we can refine and narrow our search to find the best hyperparameters and use grid sampling to do so. With AutoML, we can increase the number of iteration allowing us to go through more models supported by AutoML for classifcation. Trying more models will help us find the best model for the problem in hand.
