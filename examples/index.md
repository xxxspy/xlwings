---
layout: page
title: "Examples"
---

## Examples

### Instructions

1. Download the zip-file
2. Extract the zip file (Windows: Right-Click > Extract All... > Extract / Mac: Double-click the zip-file)
3. Open the Spreadsheet in the unzipped folder

**Note**: Lite examples require a Python installation with xlwings >=v0.7.0. Standalone versions currently only run on Windows.

### Downloads

**Example 1: Fibonacci Sequence**

This is the simplest possible example demonstrating the calculation of the Fibonacci sequence.

* **Lite (Win & Mac):** [fibonacci.zip][] (41 KB) - Dependencies: Python, xlwings
* **Standalone (Win):** [fibonacci_standalone.zip][] (14.6 MB)

[fibonacci.zip]: https://bitbucket.org/zoomeranalytics/xlwings_examples/downloads/fibonacci.zip
[fibonacci_standalone.zip]: https://bitbucket.org/zoomeranalytics/xlwings_examples/downloads/fibonacci_standalone.zip

**Example 2: Monte Carlo Simulation**

This example shows the computational power of Python by performing a Monte Carlo simulation of the price development of
a financial asset. Prices are assumed to follow a log-normal distribution.

* **Lite (Win & Mac):** [simulation.zip][] (52 KB) - Dependencies: Python, xlwings, NumPy

**Example 3: Database - Windows only**

This example shows how easy it is to work with databases. It uses [Chinook][], a popular [SQLite][] sample
database.

* **Lite (Windows only!):** [database.zip][] (392 KB) - Dependencies: Python, xlwings

**Example 4: Google Analytics Dashboard**

Please follow this [blogpost][] that guides through the example in detail!

* **Lite (Win & Mac):** [ga_dashboard.zip][] (70 KB) - Dependencies: Python, xlwings, google-api-python-client, python-gflags

**Example 5: Matplotlib**

* **Lite (Win & Mac):** [mpl.zip][] (173 KB) - Dependencies: Python, xlwings, matplotlib

**Example 6: User Defined Functions (UDFs) - Windows only**

* **Lite (Win):** [udf.zip][] (53 KB) - Dependencies: Python, xlwings, matplotlib


[Chinook]: http://chinookdatabase.codeplex.com/
[SQLite]: http://sqlite.org/
[database.zip]: https://bitbucket.org/zoomeranalytics/xlwings_examples/downloads/database.zip
[database_standalone.zip]: https://bitbucket.org/zoomeranalytics/xlwings_examples/downloads/database_standalone.zip
[blogpost]: http://blog.zoomeranalytics.com/google-analytics/

[simulation.zip]: https://bitbucket.org/zoomeranalytics/xlwings_examples/downloads/simulation.zip
[ga_dashboard.zip]: https://bitbucket.org/zoomeranalytics/xlwings_examples/downloads/ga_dashboard.zip
[mpl.zip]: https://bitbucket.org/zoomeranalytics/xlwings_examples/downloads/mpl.zip
[udf.zip]: https://bitbucket.org/zoomeranalytics/xlwings_examples/downloads/udf.zip

### Lite Versions

These versions are small in size but require an installation of Python with **xlwings >=v0.7.0**. It is highly recommended to install
one of the following scientific Python distributions as they already contain most of the necessary packages used in the
examples, most importantly pywin32, numpy, scipy and pandas.

* [Anaconda](https://store.continuum.io/cshop/anaconda/)
* [WinPython](https://winpython.github.io/) (see Notes below)
* [Canopy](https://www.enthought.com/products/canopy/)
* [Python(x,y)](https://code.google.com/p/pythonxy/)


### Standalone Versions

These versions run out-of-the-box after unzipping without any dependencies but are bigger in size.


### Notes

**WinPython**: Since WinPython doesn't change the PATH environment variables, you either have to add the location
  of the Python interpreter to the PATH manually or change the directory in the spreadsheet as follows:

* Press `Alt-F11` to fire up the VBA Editor
* Double-click the `xlwings` module
* In the `RunPython` function, change `PYTHON_DIR = ""` to the directory of where `python.exe` is, e.g.:
`PYTHON_DIR = "C:\WinPython-64bit-2.7.6.3\python-2.7.6"`
