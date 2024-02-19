# Problem_set_7_Bayes2

This week we will explore Confidence the Monte Carlo. This is primarily covered in the second half of the lectures for this week (~slide 90)

In the lecture we covered conducting a monte carlo for finding the theta associated with flipping a coin. 


# Background

Genetic variants are considered rare in the human population if they have a frequency of < 0.05 or 5%. You are attempting to find the frequency of a SNP called RS12 in the United States Population. However, you only have 90 samples from various cities across the US. This data is stored in the file. 

# Question Set A

You get the frequency data and decide to observe the dataset. Plot the frequency data in a histogram

## Question A1
Does the frequency data look normally distributed?

## Question A2
What is the mean frequency of RS12 across all sample locations?

&nbsp;

# Question Set B 

Possible values for the true frequency of the RS12 SNP could be 0.02, 0.03, 0.04, 0.05, 0.06 or 0.07. 

You hypothesize that the true frequency of RS12 is <= 0.05. Your null hypothesis is that the RS12 frequency is > 0.05. You are going to test this using the Bayes Box framework for hypothesis testing. 

You are going to use a non-informative prior. This means that your alternative and null hypotheses each have a total of 0.50 (or 50%) probability. 

## Question B1 

What prior values will you use for the possible frequencies of RS12

## Question B2 

Given your observations, what is the log-likelihood of an RS12 frequency of 0.05?




