# The Gaussian
Now that we have isolated our peak data, we can create a function which will help us find the parameters which describe it. For this, we'll first need to understand the equation that relates to it, here known as a **Gaussian** (or **Normal**) **Distribution**, which has the form:
$$f(x)=\frac{1}{\sqrt{2\pi \sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}+D$$
A Gaussian distribution describes a symmetric, bell-shaped curve centered at a mean value, $\mu$ (or mu), with its width determined by the standard deviation, $\sigma$ (or sigma), and its offset above the x-axis given by **D** (called the y-offset). 

In gamma spectroscopy, we are using the Gaussian as a model for how our detected energy counts are spread around the central photopeak. Variations in the emission and detection of our photons have caused the recorded values to "smear" into a normal distribution, with the most common value being the center of the curve. Fitting our data to this curve then allows us to extract the value for the central energy, $\mu$, as well as its margin of error.

In our equation, the first term ($\frac{1}{\sqrt{2\pi \sigma^2}}$) is called the **normalization constant**. Its purpose is to set the value of the integral of our curve to be equal to 1, meaning 100% of the data fits under the curve, but this term can actually be dropped for our purposes. We can thus set our equation to be equal to:
$$f(x)=A \cdot e^{-\frac{(x-\mu)^2}{2\sigma^2}}+D$$
In this equation:

* A controls the **height**/**amplitude** of the peak

* $\mu$ is the **mean value** in the **center** (the energy of the photon)

* $\sigma$ relates to the standard deviation

* D is the y-offset.

In order to get started using `curve_fit`, we'll first have to create a function for this equation which we will then be able to use later. So, let's create a `gaussian` function which simply returns our equation $f(x)$:
```python
def gaussian(x, amplitude, mu, sigma, y_offset):
    return amplitude * np.exp(-((x-mu)**2) / (2 * sigma**2)) + y_offset
```
Additionally, our data will include some peaks which are so close to each other that they actually **overlap**. Overlapping peaks are common when two gamma emissions have close energies. This can be modelled using the equation:
$$f(x)=A_1 \cdot e^{-\frac{(x-\mu_1)^2}{2\sigma^2_1}}+A_2 \cdot e^{-\frac{(x-\mu_2)^2}{2\sigma^2_2}}+...+A_n \cdot e^{-\frac{(x-\mu_n)^2}{2\sigma^2_n}}+D$$
Where `n` is given by the number of overlapping peaks. Luckily, our data shouldn't include more than two overlapping peaks, so we can create the second function:
```python
def double_gaussian(x, amp_1, mu_1, sigma_1, amp_2, mu_2, sigma_2, y_offset):
    return (
        amp_1 * np.exp(-((x-mu_1)**2) / (2 * sigma_1)**2) 
        + (amp_2 * np.exp(-((x-mu_2)**2) / (2 * sigma_2)**2)) 
        + y_offset
    )
```