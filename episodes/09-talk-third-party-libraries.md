---
title: (Talk) Third Party Libraries
teaching: 20
exercises: 0
break: 0
---

::::::::::::::::::::::::::::::::::::: instructor

Estimated: 13:30-13:50

Source: https://fdmrwth.pages.rwth-aachen.de/rdm-overview/modules/coding/third_party_libraries.md

:::::::::::::::::::::::::::::::::::::

## Libraries

A library is a collection of files (called modules) that contains code for use by other
programs. In addition to functions, a library can contain classes, constants, and other
elements so that you don't have to write them yourself. Libraries simplify life for programmers,
in that they provide reusable functions and classes which can be used to build applications.

## The Python Standard Library

The Python Standard Library is a collection of modules that come pre-packaged with Python.
These modules provide a wide range of functionality, including file I/O, networking, data
processing, and more. Some of the most commonly used modules in the Python Standard Library
include:

1. **os**: Provides a way to interact with the operating system, such as reading and writing files,
   creating directories, and more.
2. **sys**: Contains functions and variables that are used to manipulate the Python runtime
   environment.
3. **math**: Provides mathematical functions and constants, such as trigonometric functions,
   logarithms, and more.
4. **datetime**: Contains classes for working with dates and times.
5. **random**: Provides functions for generating random numbers.
6. **re**: Provides support for regular expressions.
7. **json**: Provides functions for encoding and decoding JSON data.

You can find a complete list of modules in the Python Standard Library in the official
[Python documentation](https://docs.python.org/3/library/index.html).

### How to Use the Python Standard Library

To use a module from the Python Standard Libary, we use the keywork `import` followed by the
name of the module. For example, to use the `os` module, we would write:

```python
import os

# Now we can use functions from the os module
print(os.getcwd())  # Print the current working directory
```

## Third Party Libraries

Third-party libraries in Python are external packages that provide additional functionality beyond
the standard library. These libraries are created and maintained by the community or other
organizations, allowing developers to leverage pre-built code for various tasks, such as data
analysis, web development, machine learning, and more. Some popular third-party libraries include:

1. **NumPy**: For numerical computing.
2. **Pandas**: For data manipulation and analysis.
3. **Matplotlib**: A plotting library for creating static, animated, and interactive visualizations in Python.
4. **SciPy**: For scientific and technical computing.
5. **pytorch**: For deep learning and neural networks.

### How to Import Third-Party Libraries

Unlike the Python Standard Library, third-party libraries are not included with Python by default.
In order to access their functionality, you need to install them separately using a package manager
like `pip` or `conda`. Once installed, you can import the library into your Python script using the
`import` statement.

#### Dependencies

A benefit / complication of third-party libraries is that they often rely on other third-party
libraries in order to function. `pandas`, for example, relies on `numpy`. When you install `pandas`,
`numpy` will be installed as well. `pip` and `conda` are package managers that help manage these
dependencies, automatically installing the required version of a library and its dependencies.

#### Package Managers

- **pip**: The Python Package Installer, `pip`, is the default package manager for Python. It is used
  to install, upgrade, and manage Python packages. You can install a package using `pip` by running
  `pip install package_name` from the command line.

- **conda**: Conda is a package manager that is commonly used for data science and scientific computing.
   It can be used to install Python packages as well as other software packages. You can install a package
   using conda by running `conda install package_name` from the command line.

#### Environment Management

When working with third-party libraries, it is often a good practice to create a virtual environment
for your project to ensure that you are using the correct versions of the libraries and their
dependencies.

This is less imporant when first starting up, but as you start to work on multiple projects, you
may find that different projects require different versions of the same library. Virtual
environments help to manage these dependencies and avoid conflicts between projects.

Some common tools for creating virtual environments include `venv`[^1], `conda`[^2], and `poetry`[^3].

[^1]: https://docs.python.org/3/library/venv.html
[^2]: https://docs.conda.io/projects/conda/en/latest/index.html
[^3]: https://python-poetry.org/


### Using Third-Party Libraries

To use a third-party library in your Python project, you typically need to follow these steps:

1. **Install the Library**:
   Before you can import a third-party library, you need to install it using a package manager
   like `pip` or `conda`. You can do this from the command line or terminal.

   Example:

   ```bash
   conda install numpy  # Install the NumPy library
   ```

2. **Import the Library in Your Code**:
   Once installed, you can import the library into your Python script using the `import` statement.

   Example:

   ```python
   import numpy as np  # Importing NumPy with an alias

   # Now you can use NumPy functions
   array = np.array([1, 2, 3])
   print(array)
   ```

3. **Using Specific Functions or Classes**:
   If you only need specific functions or classes from a library, you can import them directly.

   Example:

   ```python
   from numpy import array  # Importing the array function from NumPy

   # Now you can use the array function directly
   my_array = array([4, 5, 6])
   ```

### Tips for Managing Third-Party Libraries

- **Virtual Environments**: It's often a good practice to create virtual environments (using `venv`
  or `virtualenv`) for your projects to manage dependencies separately and avoid conflicts between
   different projects.

- **Requirements File**: You can create a `requirements.txt` file listing all your project's
- dependencies. This allows others (or yourself) to install all required packages easily using:
  ```bash
  pip install -r requirements.txt
  ```
