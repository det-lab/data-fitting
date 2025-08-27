# Introduction
Curve fitting is one of the most powerful tools available to us in modern computing. Curve fitting describes the process of matching multiple data points with an equation while finding values to describe the equation's parameters as well as their margins of error. 

In this lesson, we're going to demonstrate how to perform a curve fit using data taken at the University of Colorado Denver from a gamma spectroscopy lab. The data will include 6 radioactive isotopes with known emission spectra as well as a 7th unknown radioactive source. In the process, we will learn how to create a function which can fit a **Gaussian curve** for each of the known source's **photopeaks**. The information from those fits will then be used to find a final line which can help us determine the properties of the unknown source. We will then learn about how to perform a $\chi^2$ (chi-squared) fit in order to determine how well our predictions for the unknown source fit our data.

>If you are new to programming, it's recommended that you first take a few minutes to go over [this short lesson](https://det-lab.github.io/reading-documentation/) talking about how to read technical documentation.

--- 

Let's get started. [Click here to continue on to the next section](01_setup.md) where we will begin setting up our computers for this analysis.