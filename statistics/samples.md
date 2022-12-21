### samples are the type of data which we know the length


> let sample mean and variance be
$$
\begin{align*} 
 \overline{x} = 
 \frac{\sum_{i=0}^n x_i}{k}
 \\
 \overline{\sigma^2} = 
 \frac{\sum_{i=0}^n (x_i - \overline{\overline{x}})^2}{k}
 \end{align*}
$$

> lets say we take variance of the data generated from mean for each samples in the population

<br>
> c++ routine to calc sample mean and variance

```c
float sample_mean(float *data, size_t size)
{
	float sum = 0;
	for(size_t=0;i<size;i++)
		sum = sum + data[i];
	return sum/size;
}

float sample_variance(float *data, size_t size)
{
	float sum = 0;
	auto mean = sample_mean(data,size);
	for(size_t=0;i<size;i++)
		sum = sum + (data[i]-mean)*(data[i]-mean);
	return sum/size;
}
```