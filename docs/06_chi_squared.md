# What is a $\chi^2$ Fit?
A $\chi^2$ (or **chi-squared**/**weighted least squares** fit) is a way of fitting a model to data when each point has a different uncertainty. 

If your data points are $(O_i, C_i)$, (where O is your **Observation** data, and C is your **Calculated** or expected data) and each $O_i$ has an uncertainty $\sigma_i$, then the best-fit line **minimizes** the quantity:

$$\chi^2 = \sum_{i}(\frac{O_i - C_i}{\sigma_i})^2$$

# Why Use a $\chi^2$ Test?
Now that we've predicted the emission energies of the unknown peaks and identified possible isotopic matches using gamma emission tables, we need a way to quantify how well each candidate matches our observations. This is where the $\chi^2$ test becomes valuable. We are able to run the test by setting $O_i$ as the measured energy from the sample, $C_i$ as the known emission energy from the candidates, and $\sigma_i$ as the uncertainty in $O_i$. This means that we are performing a weighted fit: the smaller an observations uncertainty, the more it will matter for determining the quality of the fit.

For each combination of candidate isotopes, we'll compute the total chi-squared value. Once we calculate $\chi^2$, we can then also calculate the **reduced chi-squared** statistic. This lets us move beyond eyeballing the tables and actually rank our findings based on how statistically compatible they are with the observed data.:

$$\chi^2_{red}=\frac{\chi^2}{\nu}=\frac{\chi^2}{N-p}$$

Where:

* $N$ is the number of data points

* $p$ is the number of fitted parameters

* $\nu$ is the **degrees of freedom**

We'll perform a $\chi^2$ calculation for each possible **pairing** between a peak-1 candidate and a peak-2 candidate. The closer $\chi^2_{red}$ is to 1, the better the match. Large values indicate a poor match, while very small values might suggest that our uncertainties are too large or that the candidate is suspiciously good. For each of our possible 6 pairs, we'll compare their known emission energies to our observed values. So, for each pair we will compute:

$$\chi^2 = (\frac{E_{obs,1}-E_{cand,1}}{\sigma_1})^2 + (\frac{E_{obs,2}-E_{cand,2}}{\sigma_2})^2$$

Because we're not fitting any parameters, only testing two fixed candidate emission energies, the degrees of freedom, $\nu$, is simply 2, giving us:

$$\chi^2_{red}=\frac{\chi^2}{2}$$

# Implementing the $\chi^2$ calculation
The first thing that we'll want to do is place our candidate isotopes into arrays so that we can later use nested `for loops` to compare them all against each other:
```python
peak_one = [
    ('Pm-144', 696.490),
    ('Nb-94', 702.622)
]

peak_two = [
    ('Sn-123', 1088.64),
    ('Te-121', 1102.15),
    ('Zn-65', 1115.55)
]
```
We'll also want to place our predicted energies and their respective uncertainties into a similar array for this:
```python
unknown_energies = [
    (predicted_energies[0], predicted_uncertainty[0]),
    (predicted_energies[1], predicted_uncertainty[1])
]
```
Next, we can create a function which takes these arrays as inputs and returns which combination of isotopes is our best fit. Before the nested `for loop` mentioned, we'll want to create an empty array which we can fill with our results. Then, for each choice in `peak_one`, we'll go through each option in `peak_two` and select the observed/predicted energies, their uncertainties, and the candidate energies, loading them all into separate arrays which we can then use to calculate $\chi^2$. We'll load the results into the results array, and then when the loop is completed we will sort it by $\chi^2_{red}$. Then we can run this function and print out the results!
```python
def find_best_isotope_pair(unknown_energies, peak_one, peak_two):
    results = []
    for peak1_isotope, peak1_energy in peak_one:
        for peak2_isotope, peak2_energy in peak_two:
            observed = np.array([unknown_energies[0][0], unknown_energies[1][0]])
            uncertainty = np.array([unknown_energies[0][1], unknown_energies[1][1]])
            expected = np.array([peak1_energy, peak2_energy])

            residuals = (observed - expected) / uncertainty
            chi2 = float(np.sum(residuals**2))
            chi2_reduced = chi2 / len(observed)

            results.append((
                (peak1_isotope, peak2_isotope),
                (peak1_energy, peak2_energy),
                chi2,
                chi2_reduced
            ))
    results.sort(key=lambda x: abs(x[3]-1))
    return results

results = find_best_isotope_pair(unknown_energies, peak_one, peak_two)
print(f'Best fit pair: {results[0][0]}, chi-squared reduced: {results[0][3]}')
print(f'Worst fit pair: {results[-1][0]}, chi-squared reduced: {results[-1][3]}')
```
**Output:**
```python
Best fit pair: ('Nb-94', 'Zn-65'), chi-squared reduced: 0.72
Worst fit pair: ('Pm-144', 'Te-121'), chi-squared reduced: 0.11
```
# Conclusion
In this lesson, we've explored the fundamentals of data fitting. Data fitting is a crucial tool in scientific computation that allows us to extract meaningful patterns, validate hypotheses, and quantify uncertainties in experimental data. Whether you're comparing theory to experiment, identifying trends, or modeling physical systems, fitting lets you move from raw data to interpretable results.

We introduced two powerful fitting methods in Python: `linregress`, a quick and simple tool for linear fits, and `curve_fit`, a more flexible option for fitting arbitrary functions to data. We also discussed the importance of weighting data points based on their uncertainties, which led us to the reduced $\chi^2$ test. By applying this test, we demonstrated how to judge our fits using statistical evidence. 

Altogether, you've now seen how Python tools and statistical reasoning can come together to support robust data analysis. As your datasets grow more complex, these skills will form a foundation for more advanced modeling, error propagation, and hypothesis testing.