# Problem_set_7_Bayes2

This week we will explore Confidence the Monte Carlo. This is primarily covered in the second half of the lectures for this week (~slide 90)

In the lecture we covered conducting a monte carlo for finding the theta associated with flipping a coin. 


# Background

Genetic variants that are under balancing selection often have a frequency in the population of ~ 50%. You are attempting to find the frequency of a SNP called RS12 in the United States Population. However, you only have 90 samples from various cities across the US. This data is stored in the file. 

# Question Set A

You get the frequency data and decide to observe the dataset. Plot the frequency data in a histogram.

## Question A1
Does the frequency data look normally distributed?

## Question A2
What is the mean frequency of RS12 across all sample locations? 

&nbsp;

# Question Set B 

Possible values for the true mean of the RS12 SNP frequency could be 44%, 46%, 48%, 50%, 52%, or 54%

You hypothesize that the true mean frequency of RS12 is <= 50%. Your null hypothesis is that the mean RS12 frequency is > 50%. You are going to test this using the Bayes Box framework for hypothesis testing. You are testing if the mean of the distribution of frequencies is <= 50%. 

We will only be estimating the mean. Therefore, you can assume the true standard deviation is 16.

You are going to use a non-informative prior. This means that your alternative and null hypotheses each have a total of 0.50 (or 50%) probability. 

## Question B1 

What prior values will you use for the possible frequencies of RS12?

## Question B2 

Given your observations, what is the log-likelihood of observing the first city's RS12 frequency (34.28703) if the true mean of the frequencies is 50%?

&nbsp;

# Question Set C

You now want to calculate the posterior probability for every proposed value of RS12 frequency. You will need to create a loop that sums the log-likelihood for each frequency value across all observations. 

## Question C1 

What is the _total_ log-likelihood of an RS12 frequency of 50% across all the observations? 

## Question C2

Now, you will compute the posterior probability for each proposed value of RS12 frequency. To do this you will adjust your likelihood values using code such as ```lik = exp(log_lik - max(log_lik))*1000```

Then, you will compute the posterior probability using the Bayes formula and your prior values. 

What value of RS12 frequency has the highest probability? 

## Question C3

What is the sum of the probabilities for the hypothesis that RS12 <=50%

## Question C4

Does this analysis support the hypothesis that RS12 <=50%?

&nbsp;

# Question Set D

We would like a more precise estimate of our frequency based on the data. To do this we will construct a Monte Carlo to sample different frequency values. This will be the setup for our Monte Carlo 

Starting frequency = 0.5
Step 1: Calculate the likelihood for the proposed theta
Step 2: Multiply the likelihood by the prior which will be **a beta distribution with **
Step 3: Compare the ratio! of the new value with the previous value, if it has a greater value you keep the proposed theta. 
If the new value is less than the previous value, accept it with 50% success
Step 4: Propose a new theta either going up or down by a RANDOM amount



