# Homework No 5 - _From Notebooks to Research Packages_

* **Statistics 159/259, Spring 2022**
* **Due Wednesday 04/13/2022, 1:59PM PT**
* Prof. F. Pérez and GSI F. Sapienza, Department of Statistics, UC Berkeley.
* This assignment is worth a maximum of **30 points**.
* Assignment type: **individual**.

For this assignment, you will take use the [LIGO Gravitational Wave Detection Tutorial Notebook](https://github.com/losc-tutorial/LOSC_Event_tutorial/blob/master/index.ipynb) and companion files that are publicly available on Github. With those, you will structure this repository as a reproducible research package, with installable utilities separated into a small Python package, a Conda Environment specification and a new Binder link.

While the LIGO Open Science Center did a remarkable job offering these notebooks along with supporting code and a usable Binder link, we want you to make some improvements on top of this foundation, for example making certain versions explicit to ensure long-term reproducibility, more cleanly separating the supporting utilities from the code, etc.

## Deliverables

### [5 points] Repository structure

You will add to your repository, from the original LIGO one, only the following data files (we're going to focus on the GW150914 event, to keep the repository a bit smaller, so we won't include the data for other events):

```
BBH_events_v3.json
GW150914_4_template.hdf5
H-H1_LOSC_4_V2-1126259446-32.hdf5
L-L1_LOSC_4_V2-1126259446-32.hdf5
```

From the original repo, you will also need the `index.ipynb` notebook as well as the `readligo.py` utility Python file. Note that later (see below), you will be required to move the Python file into a separate package for installation.

**Important:** Add the following paragraph to the beginning of the `index.ipynb` notebook so that anyone who finds this repo clearly knows where the original credit for this content goes to:

```
**Note:** This repository is public so that Binder can find it. All code and data is based on the original [LIGO Center for Open Science Tutorial Repository](https://github.com/losc-tutorial/LOSC_Event_tutorial). This repository is a class exercise that restructures the original LIGO code for improved reproducibility, as a homework assignment for the [Spring 2022 installment of UC Berkeley's Stat 159/259 course, _Reproducible and Collaborative Data Science_](https://ucb-stat-159-s22.github.io). Authorship of the original analysis code rests with the LIGO collaboration.
```

**Tag:** you must add a git tag to the repo at this stage called `repo-basic`.

### [10 Points] A working `ligo` Conda environment

You will add to this repository an `environment.yml` file that creates an environment named `ligo`, and installs the necessary dependencies to properly run this notebook on our hub. A few important things to keep in mind:

* The LIGO notebook was written for Python 2.7, _not_ 3.x.  You will need to explicitly list Python 2.7 in your environment.

* Take advantage of the LIGO Binder to experiment with which versions of various packages it uses, so that you can add those same ones to your environment (in their original specification, they did not list specific Python versions, so they are frozen in time somewhat by accident based on when the Binder was last built).

* To find a package version, you can print its `__version__` attribute after importing it in a Python environment. At the command line, you can also see the available packages in your system using `mamba list` and `pip list` respectively (depending on whether they were installed with mamba/conda or pip).

* If a package on Binder has version say `1.2.3`, in your environment file you should request only `1.2`, _without_ the third digit. Some revision versions (the three version digits are normally known as major.minor.revision) may not always be available identically today, so it's a bit safer to request version X.Y than to try to get X.Y.Z and have it fail because Z is not available.

* Be careful with one package that you will need to list explicitly in addition to the scientific libraries and ipykernel: `decorator`. Check its version on Binder.  If you don't request it by X.Y version, you will accidentally get a much newer version that is not compatible with Python 2.7!

* Remember to install the environment for yourself, add its kernel, and start running the notebook on the hub in that environment.

**Tag:** when you complete this stage, add a tag called `conda-env`.

### [5 points] Python `ligotools` package

The notebook as shipped by LIGO includes a companion script, `readligo.py` with some data reading utilities.  You will move this file from being next to the notebook into a folder called `ligotools` and change the notebook line that reads

```python
import readligo as rl
```

into

```python
from ligotools import readligo as rl
```

For this, you will need the `ligotools` folder to work as a proper Python package (as discussed in lecture on April 6th.  Note that at this stage, you do _not_ need to write a separate `setup.py` file to make it pip-installable, only that the notebook can run with the code in the second form just above.

**Tag:** at this stage, add a tag called `ligotools-pkg`.

### [10 points] Add Binder support

Once you have everything working using the `ligo` environment on the hub, test that your repository also works on Binder.  Then, add a Binder badge to your `README.md` file so that anyone who visits your repo on Github can click on the badge and get taken to a running Binder. That Binder session should:

1. Land on the JupyterLab interface by default.
2. Have your main `index.ipynb` notebook already open.

The Binder documentation explains how to achieve both of these goals.

You _must_ test that the binder actually works and that your notebook can run to completion in the  Binder, just like the original LIGO binder did, as the instructors will use the Binder links to test your work and look at your repo.

**Tag:** at this stage, add a tag called `binder`.
