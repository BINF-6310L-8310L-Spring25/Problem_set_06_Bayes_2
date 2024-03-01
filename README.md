# Problem_set_7_Bayes2

This week we will explore Confidence the Monte Carlo. This is primarily covered in the second half of the lectures for this week (~slide 90)

In the lecture we covered conducting a Monte Carlo for finding the theta associated with flipping a coin. This week we will build a Monte Carlo to sample various mean values from a normal distribution. 

&nbsp;

# Background

Genetic variants that are under balancing selection often have a frequency in the population of ~ 50%. You are attempting to find the frequency of a SNP called RS12 in the United States Population. However, you only have 90 samples from various cities across the US. This data is stored in the file. 

&nbsp;

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

We will only be estimating the mean. Therefore, you can assume the **true standard deviation is 30**.

You are going to use a non-informative prior. This means that your alternative and null hypotheses each have a total of 0.50 (or 50%) probability. 

**NORMAL LIKELIHOOD**

To calculate the likelihood of an observation drawn from a normal distribution, we need to know how to calculate the likelihood! 

To get the _total_ likelihood for a set of observations, you can use the function below that will give you the total likelihood of a set of observations (dat) for a given single mean value (mu) for a single standard deviation (stdd)

```
normalF <- function(dat,mu,stdd) {
  # Likelihood of a normal distribution
  # dat - input data
  # mu - mean
  # stdd - standard deviation 
  sum((1/(sqrt(2*pi*stdd)))*exp(-(((dat-mu)^2)/(2*stdd^2))))
}

```

## Question B1 

What prior values will you use for the possible frequencies of RS12 (i.e., 44%, 46%...)?

## Question B2 

Given your observations, what is the likelihood of observing the first city's RS12 frequency (38.45936) if the true mean of the frequencies is 50%?

&nbsp;

# Question Set C

We are now going to use what we built above to test our two hypotheses. Hypothesis 1 is that our true frequency is 44%, 46%, 48%, or 50%. Our alternative hypothesis is that the true frequency is 52% or 54%.

## Question C1 

What is the _total_ likelihood of an RS12 frequency of 50% across all the observations? 

## Question C2

Now, you will compute the posterior probability for each proposed value of RS12 frequency. To do this, you will compute the total likelihood for each proposed frequency value. Then you Then, you will compute the posterior probability using the Bayes formula and your prior values. 

What proposed value of RS12 frequency has the highest probability? 

## Question C3

What is the sum of the probabilities for the hypothesis that RS12 <=50%

## Question C4

Does this analysis support the hypothesis that RS12 <=50%?

&nbsp;

# Question Set D

We would like a more precise estimate of our frequency based on the data. To do this, we will construct a Monte Carlo to sample different frequency values. This will be the setup for our Monte Carlo 

But first, Let's calculate the joint likelihood of a starting value of 20 for the RS12 frequency. 

## Question D1

What is the total likelihood across all cities for a mean frequency of 20? You will use the function we created above and a standard deviation of 30. 

## Question D2

We also want to set a prior probability for each frequency. Our frequency fits a beta distribution nicely since it ranges from 0-100 (or 0 to 1 if we divide by 100.) To get our prior distribution we will take the frequency and divide it by 100. Then, use the dbeta with an alpha of 2 and a beta of 2. Something like ```dbeta((proposed_lik/100),2,2)```

What is the prior value of our proposed frequency of 20?

## Question D3

What is the joint likelihood (prior * likelihood) of a mean RS12 frequency of 20? 

This is your starting value for your Markov Chain! 

&nbsp;

# Question Set E

Now, we are going to build a Markov Chain now that you know how to compute the posterior probability for any proposed frequency value. 

- Starting frequency = 20%
- Step 1: Test if the current frequency is 100 or 0. If it is, then you should move away from 100 or 0
- Step 2: Propose a new frequency by randomly going up or down by a RANDOM amount determined by rnorm(1,0,sd=5)
- Step 3: Check to make sure the new proposed frequency is not >100 or < 0 (if so, then set to 100 or 0)
- Step 4: Calculate the likelihood of the proposed frequency (using the our likelihood function)
- Step 5: Multiply the likelihood by the prior, which is our beta distribution. 
- Step 6: Compare the ratio! of the new value with the previous value, if it has a greater value you keep the proposed frequency. If the new value is less than the previous value, accept it with 50% success.

Run your Monte Carlo for 100 iterations.

## Question E1

What is the mean of your posterior frequency values after running the Monte Carlo for 100 iterations?


## Question E2

Now run your Monte Carlo for 10,000 iterations. What is the mean of your posterior frequency values?

## Question E3

We want to understand how our prior is impacting our results. Let's add a non-centrality parameter to our prior distribution. This will be ``ncp=10``. Our prior now looks like this:

![image](https://github.com/BINF-6310L-8310L-Spring24/Problem_set_7_Bayes2/assets/47755288/44497284-9a67-4c95-b2fa-dcd95fe7ed65)

Re-run the analysis with 10,000 iterations. 

What is the mean of your posterior distribution now? 

## Question E4

Does the prior have a strong impact on your point estimate of the true frequency? 



