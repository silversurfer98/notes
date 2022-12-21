### lets consider the following $\to$

> a population has n which $\to \infty$, samples with length k, so consider the following
<br>

| Samples  | sample mean         | sample varience            | sample SD                |
| -------- | ------------------- | -------------------------- | ------------------------ |
| $x_{1k}$ | $\overline{x_{1k}}$ | $\overline{\sigma^2_{1k}}$ | $\overline{\sigma_{1k}}$ |
| $x_{2k}$ | $\overline{x_{2k}}$ | $\overline{\sigma^2_{2k}}$ | $\overline{\sigma_{2k}}$ |
| .        | .                   | .                          | .                        |
| .        | .                   | .                          | .                        |
| .        | .                   | .                          | .                        |
| $x_{nk}$ | $\overline{x_{nk}}$ | $\overline{\sigma^2_{nk}}$ | $\overline{\sigma_{nk}}$ |

> so what is want is $\sigma^2$ for population on the above with n $\to \infty$ samples
> let sample mean and variance be in [[samples]]
<br>


> considering finite no of sample groups say $n_i$
>
> lets say we take variance of the data generated from mean for each samples in the population

$$
\begin{align*} 
 \overline{x_m} = 
 \frac{\sum_{i=0}^n \overline{x_{ik}}}{n_i}
 \\
 \overline{\sigma^2_m} = 
 \frac{\sum_{i=0}^n (\overline{x_i} - \overline{x_m})^2}{n-1}   
 \end{align*}
$$

> we can approx the above eqn as

$$
s_m^2 = \frac{s^2}{n}
$$
> where $s^2$ is from sample estimated variance of population [[Statistics - basics]]#sampleEstimatedPopulationVariance
> and $s_m^2$ is more closer to true value of population variance