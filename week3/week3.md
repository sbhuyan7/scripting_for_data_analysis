# Week 3

## Reading

* The Split-Apply-Combine Strategy for data analysis, by guru Hadley Wickham -- a paper that introduces the ideas behind plyr -- <http://vita.had.co.nz/papers/plyr.pdf>

* R for data science, particularly chapters 12 about tidy data and 21 about iteration, also by Hadley Wickham and Garrett Grolemund -- <http://r4ds.had.co.nz/>.

* The R Inferno by Patrick Burns -- Tongue in cheek (?!) epic about the horrors of R; in particular chapters 1-4 -- <http://www.burns-stat.com/documents/books/the-r-inferno/>

* Program better for fun and profit -- <https://inattentionalcoffee.wordpress.com/2017/01/13/program-better-for-fun-and-for-profit/>


## Exercises

* Simulate 1000 values from a normal distribution with mean 2 and standard deviation 1. How many percent of the samples were less than 0 or greater than 4? Is this what you would expect from theory?

* Instead, simulate 100 samples from the same distribution, and repeat the process 1000 times. (Hint: use `replicate` and set `simplify = FALSE` if you prefer working with a list rather than a matrix.) Use `plyr` and `mean` to get the mean for each replicate. Use the `quantile` function to get the 5% and 95% percentile of the means. Is this what you would expect from theory?

* Let's simulate a simple analysis of variance (of some of my favourite things). Imagine that we have two categorical variables. Use `rep`and `c` to create a vector with 20 elements each of "raindrops", "roses", and "whiskers" to be variable x. Create a response variable y, which equals 1 plus 0.5 if x is "raindrops" and 1 if x is "whiskers". Add random varition by adding 100 draws from a standard normal distribution (`rnorm(100)`). Put x and y into a data frame. Plot this data. Use `lm` and `drop1` to estimate coefficients and perform an F-test.

* Package the above analysis in a function that does the simulation and one function that does the analysis. Let the simulation function take the number of samples in each group as a parameter. Then repeat the above analysis 1000 times. Use the results to estimate the power of design. (Hint: The p-value of the test is in a component of the object you get from `drop1`. Assuming that you have saved the output of `drop1` in a variable called "drop", you can get it with: `drop$"Pr(>F)"[2]`.) Try the same thing with 10 and 7 samples per group. What is the power then?

* Make boxplots or jittered scatterplots showing a few few simulated datasets side by side. (Hint: use `facet_wrap`.) Use `ddply` or a loop to create a data frame that shows, for each replicate, average and standard deviation for each group.

* Look back at the coin toss functions from Week 1. Reimplement the `sim_data` function, but use `rbinom` instead of `sample`. (Hint: Use a binomial distribution with a trial number of one and a probability of success 0.5.) Make it take the same parameter and return its results in the same way as the original function.

* Remember in the week 1 homework when we looked at residual plots. One of the common assumptions in linear models is that the radom term, is independent and has equal variance for all values of the predictors. But what does the plot look like if that isn't the case? Simulate a regression study, where x is drawn from a uniform distribution from 0 to 1. Let y be `1 + 3 * x` and then add a normally distributed random error with mean zero. However, make it so that any value of y for x < 0.6 gets a normal distibution with standard deviation of 1, and any y with x >= 0.6 gets a normal distribution with standard deviation 2. Simulate this a couple of times, and draw the scatterplots and residual vs fitted plots. Can you see the increase for high values of x? 

* Modify the above code, and make a function that takes the point where the variance switches as a parameter. Then apply it 10 times with uniformly random cutoffs between 0 and 1. Plot the resulting scatterplot and fitted vs residuals plots. How good are you at guessing at which point the errors increase?



## Homework

The third homework is much more open-ended than the previous ones. The task is to perform design analysis by simulation of a study (actual or hypothetical) that is of interest to you. You will simulate data, implement the analysis in R, apply it to many simulated datasets, and evaluate the results. The report should include conclusions and informative statistical graphics.

You should follow, more or less, the following steps:

* Pick a potential data analysis that you know and care about. It should be reasonably simple, so if you pick something from a research project of yours, you will likely have to simplify a bit. Maybe you can focus or just one comparison.

* What kind of data have you got, or would you get? Invent a model that can simulate that kind of data. Feel free to simplify and make assumptions. For instance, if we were analyzing a linear regression problem, we would probably draw the errors from a normal distribution, even if that is an idealization.

* Think especially about the parameter of the model that will determine how big an effect there is, and the parameters that determine the variation. In a linear model context, this would be the coefficient associated with some continuous or categorical predictor. Sometimes, it's not so easy to find reasonable estimates for effects and errors. Maybe you can find something in the literature, or from existing previous data?

* Implement the analysis as you would with real data. A good thing about working with simulated data is that you can put them in a convenient form from the beginning. It will probably save you some file reading and data wranglig.

* Replicate your simulation, so that it generates hundreds or thousands of simulated datasets. Then apply your analysis to each simulated dataset. Gather the results of the simulations, and format the data for conventient summarization and plotting.

* Summarize the results. Does the analysis detect an effect when it should? How good is the estimate of the effect? Plot some of the simulated datasets to see what true effects would look like.

* Modify your simulations to generate data without any effect. How often does your analysis incorrectly detect an effect? Plot some of the no-effects datasets, to form pictures of what noise looks like.
