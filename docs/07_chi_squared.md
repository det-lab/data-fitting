# What is a $\chi^2$ Fit?
A $\chi^2$ (or **chi-squared**/**weighted least squares** fit) is a way of fitting a model to data when each point has a different uncertainty. 

If your data points are $(O_i, C_i)$, (where O is your **Observation** data, and C is your **Calculated** data) and each $O_i$ has an uncertainty $\sigma_i$, then the best-fit line minimizes the following quantity:

$$\chi^2 = \sum_{i}(\frac{O_i - C_i}{\sigma_i})^2$$

Once you calculate $\chi^2$, you can then calculate the **reduced chi-squared** statistic:

$$\chi^2_{red}=\frac{\chi^2}{\nu}=\frac{\chi^2}{N-p}$$

Where:

* $N$ is the number of data points

* $p$ is the number of fitted parameters

* $\nu$ is the **degrees of freedom**

In our case, we aren't fitting a curve. We're instead testing how well a pair of known emission values match with our predicted energies based on our calibration line. Since we have uncertainties associated with those predicted energies, a $\chi^2$ test gives us a rigorous way to evaluate the quality of each potential match. 

We'll perform a $\chi^2$ calculation for each possible **pairing** between a peak-1 candidate and a peak-2 candidate. For each of our possible 12 pairs, we'll compare their known emission energies to our observed values. So, for each pair we will compute:

$$\chi^2 = (\frac{E_{obs,1}-E_{obs,1}}{\sigma_1})^2 + (\frac{E_{obs,2}-E_{obs,2}}{\sigma_2})^2$$

We're not fitting any parameters, $\nu$ will be set to the number of data points alone, giving us:

$$\chi^2_{red}=\frac{\chi^2}{2}$$

The combination with the **lowest** value for $\chi^2_{red}$ will be considered the **best fit**.

# Implementing the $\chi^2$ calculation
To automate this process, we can use the following function in Python:
```python
def chi_squared(observed, expected, uncertainties):
    residuals = (observed - expected) / uncertainties
    return np.sum(residuals**2)
```