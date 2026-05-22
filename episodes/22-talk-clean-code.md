---
title: (Talk) Clean Code
teaching: 20
exercises: 0
break: 0
---

::::::::::::::::::::::::::::::::::::: instructor

Estimated: 13:45 - 14:00

Source: https://fdmrwth.pages.rwth-aachen.de/rdm-overview/modules/coding/clean_code.md

:::::::::::::::::::::::::::::::::::::

# Clean Code

## What exactly do you mean by "clean code"?

> "Any fool can write code that a computer can understand. Good programmers write code that humans
>  can understand."
>
> -- Martin Fowler

"Clean Coding" is a practice that aims to make code as easy as possible to understand, maintain,
and extend in the future.

Imagine that you are writing a lab notebook for yourself (or another fellow researcher) about an
experiment you are conducting. You would want to make sure that the notebook is clear, concise, and
easy to follow. You would want it to be as clear as possible the steps you took, the results you
obtained, and the conclusions you drew.

There are some general rules around writing clean code that apply to most programming languages.
These rules are not set in stone, but they are generally accepted as good practices. They are
designed to make your code easier to read, understand, and maintain.

### Clean Code is Readable

The most important aspect of clean code is readability. Code is read far more often than it is
written, so it is important to make sure that your code is easy to read and understand.

Certain languages are just by design closer to english text, and therefor easier to read, but even
in languages like Python, which is known for its readability, it is still possible to write code
that is difficult to understand. Conversely, even in languages like C, which are known for their
complexity, it is possible to write code that is easy to understand by using clear variable names
and comments.

Here's an example of some code that is difficult to read:

```python
def f(n):
    if n <= 1:
        return n
    else:
        return f(n-1) + f(n-2)
```

It might be pretty clear what this code is doing if you are familiar with the Fibonacci sequence,
but it's not immediately obvious and might take a few seconds, especially if you are not familiar
with the language. Here's the same code, but with better variable names, comments, and a docstring:

```python
def fibonacci(n) -> int:
    """
    Calculate the nth number in the Fibonacci sequence using a recursive algorithm.

    Args:
        n (int): The index of the number to calculate.

    Returns:
        int: The nth number in the Fibonacci sequence.
    """
    # The first two numbers in the Fibonacci sequence are 0 and 1 - if we get either of these
    # values, just return them
    if n <= 1:
        return n
    else:
        # For values larger than 1, the nth number is the sum of the (n-1)th and (n-2)th numbers
        # Recursively calculate the nth number in the Fibonacci sequence by calculating the
        # (n-1)th and (n-2)th numbers and adding them together.
        return fibonacci(n-1) + fibonacci(n-2)
```

### Clean Code is well commented

Comments are an important part of writing clean code, helping to explain what the code is doing,
why it is doing it, and how it is doing it. Comments can be used to explain complex or
non-obvious parts of the code, and to provide context for the code.

It is possible to over-comment code - it's not necessary to comment every line of code, especially
if the code is self-explanatory (which, if you are using good variable names, it often will be!).

An example of code that contains good comments:

```python
# Find all of the files in the directory that have a .csv extension
csv_file_list = glob.glob("*.csv")

for filename in csv_file_list:
    # Read in the data from the file
    data = pd.read_csv(filename)

    # Calculate the mean of the data grouped by the 'group_identifier' column, then reset the
    # index and rename the 'value' column to 'mean_value'.
    results = (
        data
            .groupby("group_identifier")
            .mean()
            .reset_index()
            .rename(columns={"value": "mean_value"})
    )

    # Create a new filename for the results and save them to a new file
    output_filename = Path(filename).stem + "_results.csv"
    results.to_csv(output_filename)

```

There are also a few examples of bad comments:

- It's ok to use a comment like `# TODO: this requires further investigation` to indicate that
    there is something that needs to be fixed or improved, but these have a tendency to stick
    around in code for a long time and can become noise.
- Commented out code is another common issue. It's better to use version control to keep track of
    changes to the code, rather than commenting out code that is no longer needed.
- Comments which exist just to exist. In the example above, we have the line
    `for filename in csv_file_list:`. Since we are using good variable names to begin with, it is
    clear from the code what this line is doing, and no comment is needed.


### Clean Code uses descriptive variable names

This could be considered a subset of readability, but it is so important that it deserves its own
section. Variable names should be descriptive and meaningful. They should describe as succinctly as
possible what the variable represents and what it is used for. Where possible, use full words and
avoid abbreviations. If a varaible name is too long, it might be a sign that the variable is doing
too much and should be split into multiple variables.

Some examples of poor variable names:

- `x`, `i`, `j`- these are common loop variables, but they don't tell you anything about what
    they are used for. There are exceptions[^1] to this rule, but in general, you should avoid using
    single-letter variable names.
- `temp` - why is this value temporary? What is it being used for?
- `data` - what kind of data is this? What does it represent?
- `list1` - what kind of list? Why is this the first list?

Some examples of good variable names:

- `total_value`
- `number_of_files`
- `user_id`
- `file_list` [^2]
- `experiment_results_df` [^2]

[^1]: For example, `i` and `j` are commonly used in matrix operations to represent the row and
    column indices, respectively. There are also some standard variable names that are commonly
    used and understood within some contexts, such as `G` for a network graph or `x` `y` and `z`
    for coordinates in 3D space.

[^2]: In languages that allow any value to be assigned to any variable (like Python) it is useful
    to include the type of the variable in the name. This is not strictly necessary in languages
    that require you to declare the type of the variable when you create it (like C or Java).

#### Naming Style

As a subset of variable naming, there are a couple different approaches for naming variables.

- **snake_case**: Words are separated by underscores. For example, `total_value`, `number_of_files`,
    `user_id`.
- **camelCase**: The first letter of each word is capitalized, except for the first word. For
    example, `totalValue`, `numberOfFiles`, `userId`.
- **kebab-case**: Words are separated by hyphens. For example, `total-value`, `number-of-files`, `user-id`.
- **PascelCase**: The first letter of each word is capitalized. For example, `TotalValue`, `NumberOfFiles`, `UserId`.
- **UPPERCASE**: All letters are capitalized. For example, `TOTAL_VALUE`, `NUMBER_OF_FILES`, `USER_ID`.

The specific convention you use is less important than being consistent [^1]

[^1]: There are language specific conventions - for example, Python uses `snake_case` for variable
    names and `PascelCase` for class names. JavaScript uses `camelCase` for both variable and
    class names. CSS uses `kebab-case` for class names.

### Clean Code is Maintainable

Maintainability is the ease with which code can be modified. Take this example, which is a very
common intro problem in programming:

```python
for i in range(1, 101):
    if i % 3 == 0 and i % 5 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

Now imagine that you are asked to modify this code so that it prints "Fizz" for every even number,
"Foo" for every number that is divisible by 5, and "FizzBuzz" for every number that is divisible
by 7 and 5. Also, instead of checking 100 numbers, we only want to print out the first 40. These
are simple changes, but it still requires modifying the code in multiple places.

```python
for i in range(1, 21):
    if i % 7 == 0 and i % 5 == 0:
        print("FizzBuzz")
    elif i % 2 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Foo")
    else:
        print(i)
```

So how might we rewrite this code to be more maintainable? One way might be to create a list of
rules that we can iterate over, checking each rule in turn to see if it applies to the current
number. This way, we can easily add, remove, or modify rules without having to change the core
logic of the loop.

```python
rules = [
    (lambda x: x % 7 == 0 and x % 5 == 0, "FizzBuzz"),
    (lambda x: x % 2 == 0, "Fizz"),
    (lambda x: x % 5 == 0, "Foo")
]
range = 40

for i in range(1, range+1):
    for rule, output in rules:
        if rule(i):
            print(output)
            continue

        print(i)
```

### Clean Code is DRY

DRY stands for "Don't Repeat Yourself". This is a principle that states that you should avoid
writing the same code multiple times. As a general rule, if you find yourself copying and pasting
code, you should pause and think about whether there is a better way to structure your code so that
you can reuse the same logic in multiple places.

Though copy/paste can be a quick way to get something done, it can lead to problems down the line
when it comes time to make changes. You might forget to update all the copies of the code, or you
might make a mistake in one copy that you don't make in another. Take the following example, where
someone wants to run the same analysis twice, but on different datasets:

``` python
import pandas as pd

###
### Analyse dataset from 2024-01-01
###

dataset_df = pd.read_csv("2024_01_01_dataset.csv")

# exclude records that have a placeholder value like "N/A"
filtered_df = dataset_df[dataset_df["score"] not in ["N/A", "NA"]]

# exclude records that have a score less than 5
filtered_df = dataset_df[dataset_df["score"] >= 5]

# find the mean and standard deviation of the remaining scores
mean_score = filtered_df["score"].mean()
std_dev = filtered_df["score"].std()

print(f"Dataset 2024_01_01_dataset.csv: Mean score: {mean_score}, Standard deviation: {std_dev}")

###
### Analyse dataset from 2024-02-01
###

dataset_df = pd.read_csv("2024_02_01_dataset.csv")

# exclude records that have a placeholder value like "N/A"
filtered_df = dataset_df[dataset_df["score"] not in ["N/A", "NA"]]

# exclude records that have a score less than 5
filtered_df = dataset_df[dataset_df["score"] >= 5]

# find the mean and standard deviation of the remaining scores
mean_score = filtered_df["score"].mean()
std_dev = filtered_df["score"].std()

print(f"Dataset 2024_02_01_dataset.csv: Mean score: {mean_score}, Standard deviation: {std_dev}")
```

This is a pretty short example, but you can see how as new datasets are added, the code will
quickly become unwieldy.

With some quick refactoring, we can make this code more DRY by extracting the common logic into a
function that we can reuse for each dataset, then looping over the datasets.

``` python
import pandas as pd

datasets = ["2024_01_01_dataset.csv", "2024_02_01_dataset.csv"]

def analyse_dataset(file_path: str):
    dataset_df = pd.read_csv(file_path)

    # exclude records that have a placeholder value like "N/A"
    filtered_df = dataset_df[dataset_df["score"] not in ["N/A", "NA"]]

    # exclude records that have a score less than 5
    filtered_df = dataset_df[dataset_df["score"] >= 5]

    # find the mean and standard deviation of the remaining scores
    mean_score = filtered_df["score"].mean()
    std_dev = filtered_df["score"].std()

    return mean_score, std_dev

for dataset in datasets:
    mean_score, std_dev = analyse_dataset(dataset)
    print(f"Dataset {dataset}: Mean score: {mean_score}, Standard deviation: {std_dev}")
```

This small change means that the process of updating the code to adapt to changes in processing is
much simpler - the updates would only have to be done once in the `analyse_dataset` function and
would always apply to all datasets. Additional, by defining the `datasets` list at the start of
the script, it is easy to add or remove datasets from the analysis without having to modify the
core logic of the script.

### Clean Code is Well Documented

Documentation is an important part of writing clean code. It helps other people (and your future
self) understand what the code does, why it does it, and how it does it. The documentations can
be as detailed as you are willing to make it, but at a minimum, you should include a docstring for
each function that describes what the function does, what arguments it takes, and what it returns.

There are a variety of standards for writing docstrings, both between languages and within. The
most important thing is to select a standard as stick with it. Here are some example docstrings
for a function that calculates the area of a circle:

Python:

<details>
<summary>Google Style Guide</summary>

``` python
def circle_area(radius: float) -> float:
    """Calculate the area of a circle.

    Args:
        radius (float): The radius of the circle.

    Returns:
        float: The area of the circle.
    """
    return math.pi * radius ** 2
```

</details>

<details>
<summary>Numpy Style Guide</summary>

``` python
def circle_area(radius: float) -> float:
    """Calculate the area of a circle.

    Parameters
    ----------
    radius : float
        The radius of the circle.

    Returns
    -------
    float
        The area of the circle.
    """
    return math.pi * radius ** 2
```

</details>

<details>
<summary>Sphinx Style Guide</summary>

``` python
def circle_area(radius: float) -> float:
    """Calculate the area of a circle.

    :param radius: The radius of the circle.
    :type radius: float
    :return: The area of the circle.
    :rtype: float
    """
    return math.pi * radius ** 2
```

</details>

R:

<details>
<summary>Roxygen2 Style Guide</summary>

``` r
#' Calculate the area of a circle
#'
#' @param radius The radius of the circle
#' @return The area of the circle
#'
#' @examples
#' circle_area(5)
circle_area <- function(radius) {
    return(pi * radius^2)
}
```
</details>

#### File Headers

In addition to documenting functions, it is also important to document the file itself. The exact
information will depend on the project and purpose of the file. A common script header might look
like this:

---

<h3>Scripts</h3>

With scripts in particular, it's important to include a header that describes the purpose of the
script, the author, and the date it was created or last modified. This information can help others
understand the context of the script and how it fits into the larger project.

<details>
<summary>Python</summary>

``` python
"""
01_data_cleaning.py

Author: Max Mustermann <max.mustermann@email.org>
Date: 2024-01-01

This script reads in a dataset for the <PROJECT> project and applies some basic cleaning steps
to prepare the data for analysis.

These steps include:
- Removing records with missing/invalid values
- Standardizing column names
- Converting data types
- Saving the cleaned dataset to a new file

Note: This script assumes that the dataset is in CSV format.
"""
```

</details>

<details>
<summary>R</summary>

``` r
#' Data Cleaning Script
#'
#' Author: Max Mustermann <max.mustermann@email.org>
#' Date: 2024-01-01
#'
#' This script reads in a dataset for the <PROJECT> project and applies some basic cleaning steps
#' to prepare the data for analysis.
#'
#' These steps include:
#' - Removing records with missing/invalid values
#' - Standardizing column names
#' - Converting data types
#' - Saving the cleaned dataset to a new file
#'
#' --------------------------------------------------------------------------------------------
#'
#' Notes: This script assumes that the dataset is in CSV format.
#'
#' --------------------------------------------------------------------------------------------
```

</details>

---

<h3>Modules</h3>

For modules, it is important to include a header that describes the purpose of the module and it's
intended usage. This information can help others understand how to use the objects defined in the
file and how they fit into the larger project. An example header for a module might look like this:

<details>
<summary>Python</summary>

``` python
"""
project_dataset.py

This object is used to load datasets for the <PROJECT> project for use in the model training
pipeline. It is based on the pytorch Dataset class and provides a simple interface for loading
and preprocessing data.

Usage:
    dataset = ProjectDataset(file_path="data.csv")

Parameters:
    - file_path (str): The path to the dataset file. The file must be in CSV format.
    - train (bool, optional): A flag indicating whether the dataset is for training or testing.
        Default is True.

Exceptions:
    - FileNotFoundError: If the specified file does not exist
    - ValueError: If the file is not in CSV format

"""
```

</details>

<details>
<summary>R</summary>

``` r
#' ProjectDataset: Load datasets for the <PROJECT> model training pipeline
#'
#' This object is used to load datasets for the <PROJECT> project, providing a simple
#' interface for loading and preprocessing data.
#'
#' @usage dataset <- ProjectDataset(file_path = "data.csv")
#'
#' @param file_path A string specifying the path to the dataset file. The file must be in CSV format.
#' @param train A logical value indicating whether the dataset is for training or testing. Default is TRUE.
#'
#' @return A dataset object ready for use in model training.
#'
#' @examples
#' dataset <- ProjectDataset("data.csv")
#'
#' @throws FileNotFoundError If the specified file does not exist.
#' @throws ValueError If the file is not in CSV format.
```

</details>

### Clean Code is Consistent

You might agree or disagree with some of the rules we've discussed so far, but the most important
by far is consistency. It is better to have code that is consistently formatted and styled than to
have code that is formatted and styled in the "best" way some of the time. Consistency makes it
easier to read and understand code because you know what to expect.

## Tools For Writing Clean Code

There are a number of tools available that can help you write clean code. Some of these tools are
linters, which are programs that analyze your code and flag potential issues. Others are
formatters, which automatically format your code according to a set of rules.

<h3>Linters</h3>

- **Python**: [flake8](https://flake8.pycqa.org/en/stable/)
- **Python**: [Pylint](https://pylint.readthedocs.io/en/stable/)
- **Python**: [ruff](https://github.com/astral-sh/ruff)
- **R**: [lintr](https://lintr.r-lib.org/)
- **JavaScript**: [ESLint](https://eslint.org/)
- **Java**: [Checkstyle](https://checkstyle.sourceforge.io/)
- **C/C++**: [Clang](https://clang.llvm.org/docs/ClangFormat.html)

<h3>Formatters</h3>

- **Python**: [Black](https://black.readthedocs.io/en/stable/)
- **Python**: [ruff](https://github.com/astral-sh/ruff)
- **R**: [styler](https://styler.r-lib.org/)
- **JavaScript**: [Prettier](https://prettier.io/)
- **C/C++**: [Clang](https://clang.llvm.org/docs/ClangFormat.html)
