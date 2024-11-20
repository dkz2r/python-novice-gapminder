---
title: Day 1 Recap
teaching: 15
exercises: 0
break: 00
---

::::::::::::::::::::::::::::::::::::: instructor

Estimated: 09:00 - 09:15

:::::::::::::::::::::::::::::::::::::

## Recap of Day 1

- Running and Quitting
  - Start Jupyter Lab from the "Anaconda Prompt" by typing `jupyter lab`
  - Alternatively you can start Jupyter Lab from the Anaconda Navigator
  - Jupyter Lab will start in your default web browser
  - Jupyter Lab will open in the directory where you started it

- Variables
  - Variable Names
    - can **only** contain letters, digits, and underscore `_` (typically used to separate words in long variable names)
    - cannot start with a digit
    - are **case sensitive** (age, Age and AGE are three different variables)
    - should be descriptive and meaningful

  - Variables must be assigned a value before they can be used
  - We can use indexing to access individual elements of a string
    - `hello[0]` will return `h`
  - We can use slicing to access a range of elements in a string
    - `hello[0:3]` will return `hel`

- Types and Type Conversions
  - Every value in Python has a type
  - We can use the `type()` function to find out the type of a value
  - Common types are `int`, `float`, `str`
  - We can convert between types using the `int()`, `float()`, and `str()` functions
  - We can use the `+` operator to concatenate strings or add numbers
  - Not all operators work with all types

- Libraries
  - Libraries are collections of functions that extend the capabilities of Python
  - There are a number of useful libraries that come with python
  - We can import a library using the `import` statement
  - We can use `help()` to get information about a library or a function
  - We can use `import ... as ...` to give a library a shorter alias

- Reading Tabular Data
  - We can use the `pandas` library to read tabular data
  - We can use the `read_csv()` function to read a CSV file

- Dataframes
  - We can access specific elements of a DataFrame using the `iloc` method
    - `data.iloc[0, 0]` will return the element in the first row and first column
    - `data.iloc[0, :]` will return the first row
    - `data.iloc[:, 0]` will return the first column
    - `data.iloc[0:2, 0:2]` will return the first two rows and columns

- Plotting
  - We can use the `matplotlib` library to create plots
    - `plt.plot()` will create a line plot
    - `plt.scatter()` will create a scatter plot
  - We can use the `xlabel()`, `ylabel()`, and `title()` functions to add labels to the plot
  - We can use the `show()` function to display the plot
