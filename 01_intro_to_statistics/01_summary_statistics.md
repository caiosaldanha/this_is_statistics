# Summary Statistics

1. What Is Statistics: the practice and study of collecting and analyzing data

    There are 2 main branches of statistics:

    1. Descriptive Statistics: focuses on describing and summarizing the data at hand
    2. Inferential Statistics: uses the data at hand, which is called sample data, to make inferences about a larger population
2. Types of data
    1. Numeric or Quantitative
        1. Continuous (Measured)
        2. Discrete (Counted)
    2. Categorical or Qualitative
        1. Nominal (Unordered)
        2. Ordinal (Ordered)
3. Sometimes, categorical variables are represented using numbers. However, it's important to note that this doesn't necessarily make them numeric variables.
4. Being able to identify data types is important since the type of data you're working with will dictate what kinds of summary statistics and visualizations make sense for your data
5. Measures of Center
    1. Histograms: takes a bunch of data points and separates them into bins, or ranges of values.
    2. Measures of center
        1. Mean: To calculate mean, we add up all the numbers of interest and divide by the total number of data points. (more sensitive to extreme values)

            ```python
            import numpy as np
            np.mean(df['column'])
            ```

        2. Median: is the value where 50% of the data is lower than it, and 50% of the data is higher

            ```python
            import numpy as np
            np.median(df['column'])
            ```

        3. Mode: is the most frequent value in the data.

            ```python
            import statistics
            statistics.mode(df['column'])
            ```

    3. Skew
        1. When data is skewed, the mean and median are different. The mean is pulled in the direction of the skew, so it's lower than the median on the left-skewed data, and higher than the median on the right-skewed data. Because the mean is pulled around by the extreme values, it's better to use the median since it's less affected by outliers.
6. Measures of Spread
    1. Variance: measures the average distance from each data point to the data's mean. To calculate the variance, we start by calculating the distance between each point and the mean, so we get one number for every data point. We then square each distance and then add them all together. Finally, we divide the sum of squared distances by the number of data points minus 1, giving us the variance. The higher the variance, the more spread out the data is. It's important to note that the units of variance are squared. We can calculate the variance in one step using np.var(), setting the ddof argument to 1. If we don't specify ddof equals 1, a slightly different formula is used to calculate variance that should only be used on a full population, not a sample.
    2. Standard deviation: calculated by taking the square root of the variance. It can be calculated using np.std(). Just like np-dot-var, we need to set ddof to 1. The nice thing about standard deviation is that the units are usually easier to understand since they're not squared.
    3. Mean absolute deviation: takes the absolute value of the distances to the mean, and then takes the mean of those differences. While this is similar to standard deviation, it's not exactly the same. Standard deviation squares distances, so longer distances are penalized more than shorter ones, while mean absolute deviation penalizes each distance equally. One isn't better than the other, but SD is more common than MAD.
    4. Quantiles (Percentiles):  
        1. Boxplots use quartiles
        2. Quantiles using np.linspace(start, stop, numofintervals)

            ```python
            np.linspace(start, stop, numofintervals)
            ```

            ```python
            np.quantile(df[’column’], [list of quantile])
            ```

    5. Interquartile range (IQR): It's the distance between the 25th and 75th percentile, which is also the height of the box in a boxplot. We can calculate it using the quantile function, or using the iqr function from scipy-dot-stats.

        ```python
        from scipy.stats import iqr
        iqr(df['column'])
        ```

    6. Outliers: are data points that are substantially different from the others.
        1. A rule that's often used is that any data point less than the first quartile minus 1-point-5 times the IQR is an outlier, as well as any point greater than the third quartile plus 1-point-5 times the IQR.

            $$
            data < Q1 -1.5 \times IQR 
            $$
            
            $$
            \\ or 
            $$
            
            $$
            \\ data > Q1 +1.5 \times IQR
            $$

            ```python
            from scipy.stats import iqr
            
            iqr = iqr(df['column'])
            
            lower_treshold = np.quantile(df['column'], .25) - 1.5 * iqr
            upper_treshold = np.quantile(df['column'], .75) + 1.5 * iqr
            
            df[(df['column'] < lower_treshold) | (df['column'] > upper_treshold)]
            ```

        2. All in one go

            ```python
            df['column'].describe()
            ```
