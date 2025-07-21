# Setup
This lesson will be using Python 3 along with several of its more common libraries: `scipy`, `pandas`, `matplotlib`, and `numpy`. This lesson will also be done using a Jupyter Notebook. 

First, it'll be necessary to install Python if you don't already have it. You can follow the instructions from [python's official website](https://realpython.com/installing-python/) in order to get started. 

It's recommended to install Jupyter Notebook through `pip`, so after installing Python you should check that it comes with `pip` installed. This can be done by running the following commands depending on your operating system:

|                           | Linux                        | MacOS                        | Windows                      |
|---------------------------|------------------------      |------------------------------|------------------------------|
|**Command (Check python)** |python --version              |python --version              |py --version                  |
|**Output**                 |Python 3.N.N                  |Python 3.N.N                  |Python 3.N.N                  |
|**Command (Check pip)**    |python -m pip --version       |python -m pip --version       |py -m pip --version           |
|**Output**                 |pip X.Y.Z from (python 3.N.N) |pip X.Y.Z from (python 3.N.N) |pip X.Y.Z from (python 3.N.N) |

You can then use `pip` to install either `JupyterLab` or `Jupyter Notebook` with the command:
```bash
pip install jupyterlab
```
or:
```bash
pip install notebook
```
You can then run them with either:
```bash
jupyter lab
```
or:
```bash
jupyter notebook
```
It should be noted that in order for Jupyter to work you will also be required to have an up-to-date browser. Chrome, Safari, and Firefox are all supported.

Running one of these commands will then open Jupyter in a browser. 

Jupyter will then show you an in-browser version of your file-explorer where you can navigate to create a new project folder to follow along with this lesson. Before doing that, make sure that you also have the necessary libraries installed. Click on `New` and select `Terminal` in order to ensure that the libraries are installed in the same location that Jupyter has access to. From this terminal, run the commands:
```bash
pip install scipy
pip install pandas
pip install matplotlib
pip install numpy
```
The `scipy` library will be used to find our peaks and create our curve fits, `pandas` will be used for loading the `.csv` data, `matplotlib` will be used to plot the data, and `numpy` will be used for multiple mathematical expressions.

Next, create a folder to house your project files, named something like "data-fitting". After doing this, download and unzip [these raw data files](raw-data/raw-data.zip). Then, you can move the "raw-data" folder into your project folder. 

Finally, create a new notebook by clicking on `New` and `Notebook` and selecting the kernel - `Python 3 (ipykernel)`. You can then either name your project or keep it untitled.

---

Now that we're all setup, [click here to continue to the next section](02_experiment_details.md) where we can begin to learn more about the experiment and how it functions before getting started fitting our data.