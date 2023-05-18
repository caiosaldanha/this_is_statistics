# 2. Random Numbers and Probability

1. Measuring Chance
    1. We can measure the chances of an event using probability. We can calculate the probability of some event by taking the number of ways the event can happen and dividing it by the total number of possible outcomes.
        
        $$
        P(\text{event}) = \frac{\text{number ways event can happen}}{\text{total number of possible outcomes}}
        $$
        
2. Sampling from a DataFrame

    ```python
    df.sample(n)
    ```

3. Setting a random seed
    1. To ensure we get the same results when we run the script in front of the team, we can set the random seed using np.random.seed(). The seed is a number that Python's random number generator uses as a starting point, so if we orient it with a seed number, it will generate the same random value each time. The number itself doesn't matter. We could use 5, 139, or 3 million. The only thing that matters is that we use the same seed the next time we run the script.

        ```python
        np.random.seed(n)
        ```

4. Sampling with/without replecement

    ```python
    df.sample(n, replace=True/False #default)
    ```

5. Independent events
    1. Two events are independent if the probability of the second event isn't affected by the outcome of the first event. In general, when sampling with replacement, each pick is independent.
6. Dependent events
    1. Events are considered dependent when the outcome of the first changes the probability of the second.
7. Probability distribution
    1. A probability distribution describes the probability of each possible outcome in a scenario. We can also talk about the expected value of a distribution, which is the mean of a distribution. We can calculate this by multiplying each value by its probability and summing.
    2. When all outcomes have the same probability, like a fair die, this is a special distribution called a **discrete uniform distribution.**
    3. Visualizing a sample

        ```python
        df['column'].hist(bins=np.linspace(start, stop, num_of_slices))
        plt.show() 
        ```

    4. Law of large numbers: as the size of your sample increases, the sample mean will approach the theoretical mean.
8. Continuous distributions. [scipy.stats.uniform — SciPy v1.10.1 Manual](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.uniform.html#scipy.stats.uniform)

    ```python
    from scipy.stats import uniform
    uniform.cdf(x, loc=0, scale=1) #cumulative distribution function
    ```

    1. Generationg radom numbers according to uniform distribution

    ```python
    from scipy.stats import uniform
    uniform.rvs(minvalue, maxvalue, size=#ofvalues)
    ```

    b. Other continuous distributions: No matter the shape of the distribution, the area beneath it must always equal 1.

9. Binomial Distribution: probability distribution of successes in a sequence of independent trials. [scipy.stats.binom — SciPy v1.10.1 Manual](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.binom.html#scipy.stats.binom)
    1. Binary outcomes:

        ```python
        #simulate binomial outcomes [scipy function]
        binom.rvs(# of coins, probability of heads/success, size=# of trials)
        
        from scipy.stats import binom
        binom.rvs(1, 0.5, size=8) #Flip 1 coin with 50% of success 8 times
        ```

    2. Other probabilities: We could also have a coin that's heavier on one side than the other, so the probability of getting heads is only 25%. To simulate flips with this coin, we'll adjust the second argument of binom.rvs to 0.25
    3. The binomial distribution can be described using two parameters, n and p. n represents the total number of trials being performed, and p is the probability of success. n and p are also the third and second arguments of binom.rvs

    $$
    n\text{: total number of trials}
    $$

    $$
    p\text{: probability of success}
    $$

    ```python
    binom.rvs(# of coins, p [probability of success], size = n [total number of trials])
    ```

    d. Binomial probability

    1. To get the probability of getting 7 heads out of 10 coins, we can use binom.pmf. The first argument is the number of heads or successes. The second argument is the number of trials, n, and the third is the probability of success, p. If we flip 10 coins, there's about a 12% chance that exactly 7 of them will be heads.

        $$
        P(\text{heads = num})
        $$

        ```python
        binom.pmf(num success[heads], num trials, prob of heads) #Probability Mass Function
        >> 0.1171875 #12%
        ```

    2. binom.cdf gives the probability of getting a number of successes less than or equal to the first argument. The probability of getting 7 or fewer heads out of 10 coins is about 95%.

        $$
        P(\text{heads} \le \text{num})
        $$

        ```python
        binom.cdf(num success[heads], num trials, prob of heads) #Cumulative distribution function
        >> 0.9453125 #95%
        ```

    3. We can take 1 minus the probability of getting 7 or fewer heads to get the probability of a number of successes greater than the first argument.

        $$
        P(\text{heads} \gt \text{num})
        $$

        ```python
        1 - binom.cdf(num success[heads], num trials, prob of heads) #Cumulative distribution function
        >> 0.0546875 #5%
        ```

    4. The expected value of the binomial distribution can be calculated by multiplying n times p. The expected number of heads we'll get from flipping 10 coins is 10 times 0-point-5, which is 5.

        $$
        \text{Expected value} = n \times p
        $$

    5. It's important to remember that in order for the binomial distribution to apply, each trial must be independent, so the outcome of one trial shouldn't have an effect on the next.
