# Data Fitting and Analysis in Python
This lesson introduces the foundational concepts of scientific data fitting through the lens of gamma spectroscopy. You'll learn the basics of using tools such as `find_peaks`, `curve_fit`, and `linregress` to extract meaningful insights from experimental data and quantify how well a theoretical model agrees with observations.

The project is structured with a Jupyter Notebook workflow and assumes a basic familiarity with Python. You'll be guided through setting up your environment, understanding the experiment being used as an example, and performing the analysis step by step.

# Lesson Outline
This lesson is broken into the following sections:
## Introduction (`index.md`)
A brief overview of what the lesson will cover and the role of data fitting in scientific computing.
## Setup (`01_setup.md`)
Instructions for setting up your Python environment using Jupyterlab or Jupyter Notebook, along with the required libraries.
## Experiment (`02_experiment_details.md`)
An introduction to gamma spectroscopy:

* The three main types of atomic radiation

* How scintillators, photomultiplier tubes (PMTs), and spectrometers work

* The steps involved in collecting and preparing spectral data
## Initial Plotting (`03_isolating_peaks.md`)
Starting with plotting the raw data before showing how to isolate the photopeaks. Also describes the Compton continuum and edge as well as backscatter and X-ray escape peaks.
## First Fits (`04_fitting_curves.md`)
Here you'll learn:

* What a Gaussian curve is and why it models peaks in spectroscopy

* How to define single and double Gaussian functions

* How to use `curve_fit` to extract parameters like the peak's center and uncertainty.
## Line Fit (`05_linregress.md`)
With the centers of all the radioactive sources found, you'll

* Fit a line using `linregress` to relate spectrometer channel number to gamma emission energy

* Use the linear fit to estimate the energy of the unknown peaks

* Compare these energies against known isotopic emission lines to generate candidate matches for the unknown source
## Chi Squared (`06_chi_squared.md`)
Finally, you'll quantify how well each isotopic candidate matches the unknown peaks by:

* Implementing a chi-squared test with weights based on uncertainty

* Calculate the reduced chi-squared statistic to evaluate the quality of the candidate isotopes

* Rank the candidate isotope combinations based on their statistical compatibility
# Goals
By the end of this lesson, you should be able to:

* Understand the principles of gamma spectroscopy and its data output

* Understand how to use `curve_fit` to extract parameters and their uncertainties

* Understand how to use `linregress` for calibrating scientific instruments

* Understand how to use chi-squared statistics to compare models and assess fit quality
# Requirements

* Python 3.11+

* Jupyter Notebok or JupyterLab

* Numpy, SciPy, Matplotlib, and Pandas libraries
# License
This lesson is made available under the Creative Commons Attribution 4.0 License