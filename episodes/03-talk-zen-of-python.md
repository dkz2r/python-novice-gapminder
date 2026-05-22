---
title: (Talk) The Zen of Python
teaching: 20
exercises: 0
break: 0
---

::::::::::::::::::::::::::::::::::::: instructor

If you're not familiar with Python, don't be alarmed if this looks confusing. By the end of the workshop this will all make sense. And you can always refer back to the Zen of Python by using "import this".

Name spacing is not a beginner concept so we won't talk about it in this workshop but feel free to find us in the break or email any questions to us.

Estimated: 10:30 - 10:50

Source: https://fdmrwth.pages.rwth-aachen.de/rdm-overview/modules/coding/zen_of_python.md

:::::::::::::::::::::::::::::::::::::

## What is it?

The Zen of Python is a collection of 19 "guiding principles" for writing computer programs that
influence the design of the Python programming language. These principles were written in 1999 by
software engineer Tim Peters and they emphasize **readability**, **simplicity**, and **clarity**
in code, which are core values of the Python community.

Python code that aligns with these principles is often referred to as "Pythonic".

In May 2020, Barry Warsaw (developer of GNU Mailman) wrote the lyrics to music:

[The Zen of Python](https://www.youtube.com/watch?v=i6G6dmVJy74)

## First Import

The Zen of Python is included in the Python Interpreter where you can import it anytime to review.

```python
import this
```

> Beautiful is better than ugly.
>
> Explicit is better than implicit.
>
> Simple is better than complex.
>
> Complex is better than complicated.
>
> Flat is better than nested.
>
> Sparse is better than dense.
>
> Readability counts.
>
> Special cases aren't special enough to break the rules.
>
> Although practicality beats purity.
>
> Errors should never pass silently.
>
> Unless explicitly silenced.
>
> In the face of ambiguity, refuse the temptation to guess.
>
> There should be one-- and preferably only one --obvious way to do it.
>
> Although that way may not be obvious at first unless you're Dutch.
>
> Now is better than never.
>
> Although never is often better than *right* now.
>
> If the implementation is hard to explain, it's a bad idea.
>
> If the implementation is easy to explain, it may be a good idea.
>
> Namespaces are one honking great idea -- let's do more of those!


## What does this mean?

### Beautiful is better than ugly.

Writing clean, well-structured code with proper indentation and spacing is more appealing than
cluttered, messy code.

```python
# Beautiful: Clear function name, good variable names and proper formatting
def calculate_area(radius):
    return 3.14 * radius * radius

# Ugly: Unclear function name, bad variable names and improper formatting
def a(r):return 3.14*r*r
```

**Why it Matters:** Beautiful code is easier to read, understand, and maintain. It reduces the
cognitive load on developers and makes it easier to spot errors or potential improvements.

### Explicit is better than implicit.

Clearly defining variable types or using clear function names makes it easier to understand the
code's purpose.

```python
# Explicit: Using type hints to indicate the expected types of arguments and return values
def add_numbers(a: int, b: int) -> int:
    return a + b

# Implicit: Not specifying types or using unclear variable names
def add(x, y):
    return x + y
```

**Why it Matters:** Explicit code is easier to understand and less prone to errors. It helps other
developers (and your future self) quickly grasp the purpose and functionality of the code.

### Simple is better than complex.

Using straightforward logic instead of convoluted algorithms makes code easier to maintain. If
there is a simple solution, use it.

```python
# Simple: Using a built-in function to calculate the sum of a list of numbers
total = sum(numbers)

# Complex: Manually calculating the sum of a list of numbers using a loop
total = 0
for number in numbers:
    total += number
```

**Why it Matters:** Simple code is easier to debug, test, and maintain. It reduces the chances of
introducing bugs and makes it easier to add new features or modify existing ones. Additionally,
simple code is often more performant than complex code.
For example, the `sum()` built-in function looks very simple when we use it here, but
[it's actually a very complex function that is optimized for performance.](https://github.com/python/cpython/blob/3966d8d626fc9adcdf0663024d4ae6e6be7ef858/Python/bltinmodule.c#L2649)

### Complex is better than complicated.

If a solution must be complex due to requirements, ensure it's still organized and understandable
rather than convoluted.

```python
# Complex but organized: Processing data with a helper function and a list comprehension
def process_data(data):
    if isinstance(data, list):
        return [process_item(item) for item in data]
    else:
        return process_item(data)

# Complicated
def process(data):
    if type(data) == list:
        result = []
        for i in range(len(data)):
            result.append(process_item(data[i]))
        return result
    else:
        return process_item(data)
```

**Why it Matters:** Complex code is sometimes necessary, but we should strive to make it as clear
and as organized as possible. Code is often read more than it is written, so prioritizing
readability and maintainability is crucial.

### Flat is better than nested.

Avoiding deep nesting in control structures improves readability. If you find yourself needing
multiple levels of indentation, consider a different approach to the problem.

```python
# Nested structure: Using if-else statements with excessive nesting and indentation
if user_logged_in:
    if user_is_admin:
        if user_can_edit:
            perform_edit()
        else:
            print("User does not have permission to edit")
    else:
        print("User must be an administrator for this action")
else:
    print("User is not logged in")

# Flat structure: Using if-elif-else statements without excessive nesting
if not user_logged_in:
    print("User is not logged in")
elif not user_is_admin:
    print("User must be an administrator for this action")
elif not user_can_edit():
    print("User does not have permission to edit")
else:
    perform_edit()
```

**Why it Matters:** Flat code is easier to read and understand. It reduces the cognitive load on
developers and makes it easier to follow the logic of the program. Nested structures can be
confusing and make it harder to spot errors or understand the code's flow.

### Sparse is better than dense.

Spacing out code and adding comments can enhance clarity rather than cramming everything into
fewer lines. Writing dense code or "one-liners" can be fun, but makes it much harder to read and
understand later on.

```python
# Sparse and clear
result = compute_value(x)

if result > threshold:
    print("Above threshold")

# Dense but harder to read
if(compute_value(x)>threshold): print("Above threshold")
```

**Why it Matters:** Sparse code is easier to read and maintain. It provides room for comments and
documentation, which can help other developers understand the code. Dense code can be challenging
to debug and modify, especially for those who didn't write it.

### Readability counts.

This principle speaks for itself; writing code that others can easily read and understand should
always be a priority. Clear, well-documented code is easier to maintain and debug.

```python
# Readable: Good Naming, clear comments, docstrings and proper formatting
import math

def calculate_area(radius: float) -> float:
    """
    Calculate the area of a circle given its radius.

    Args:
        radius: The radius of the circle.

    Returns:
        float: The area of the circle.
    """
    # Raise an error if the radius is negative
    if radius < 0:
        raise ValueError("Radius cannot be negative")

    # Calculate the area using the formula A = πr^2
    return math.pi * (radius **2)

```

**Why it Matters:** Readable code is easier to maintain, debug, and extend. It helps developers
quickly understand the purpose and functionality of the code.

### Special cases aren't special enough to break the rules.

Following conventions even when dealing with edge cases ensures consistency across the codebase.

```python
# Even when handling zero discounts, we still apply the same logic without special cases.
def calculate_discount(price, discount=0):
    assert discount >= 0, "Discount cannot be negative"
    return price * (1 - discount)

# Special Case: Breaking the rules for a specific case
def calculate_discount(price, discount=0):
    if discount < 0:
        # Do something special for negative discounts
        return price
    elif discount == 0:
        # Do something special for zero discounts
        return price
    else:
        return price * (1 - discount)
```

**Why it Matters:** Consistency in code makes it easier to understand and maintain. Special cases
that break the rules can introduce confusion and make the code harder to follow.

### Although practicality beats purity.

Sometimes pragmatic solutions are necessary even if they don't adhere strictly to ideal practices.

```python
def fetch_data(source):
    try:
        data = get_data_from_source(source)
    except Exception as e:  # Practicality over purity here; catching all exceptions may not be pure but is practical.
        log_error(e)
        data = default_data()
    return data
```

**Why it Matters:** While it's essential to strive for clean, maintainable code, practicality is
also important. In some cases, pragmatic solutions are necessary to handle real-world scenarios.

### Errors should never pass silently.

Always handle errors appropriately rather than ignoring them.

```python
def read_file(filename):
    try:
        with open(filename, 'r') as file:
            return file.read()
    except FileNotFoundError:
        print(f"Error: The file {filename} was not found.")
    except Exception as e:
        print(f"An error occurred: {e}")
```

**Why it Matters:** Ignoring errors can lead to unexpected behavior and make it harder to diagnose
issues. Proper error handling ensures that problems are addressed and communicated effectively.

### Unless explicitly silenced.

It's acceptable to suppress specific warnings or errors when you have a good reason to do so using
context managers or specific exception handling.

```python
import warnings

with warnings.catch_warnings():
    warnings.simplefilter("ignore")
    deprecated_function()  # Silencing specific warning intentionally
```

**Why it Matters:** Explicitly silencing warnings or errors can be useful in certain situations,
such as when dealing with deprecated code or code with known issues. However, it's important to do
so with a clear understanding of the potential drawbacks.

### In the face of ambiguity, refuse the temptation to guess.

When in doubt, be explicit and clear rather than making assumptions or guesses.

```python
# Explicit: Using named arguments to clarify the purpose of each parameter
calculate_area(radius=5)

# Ambiguous: Relying on the order of arguments, which can be confusing
calculate_area(5)
```

**Why it Matters:** Ambiguity can lead to misunderstandings. It means more typing, but it also
makes the code more readable.

### There should be one-- and preferably only one --obvious way to do it.

Strive to write code that is clear and straightforward. Try to think about things from the
perspective of someone new coming into your codebase - will this make sense to them? How much
context will they need to understand what's going on?

```python
# Obvious: Clearly named functions
def read_file(filename):
    ...

def write_file(filename, data):
    ...

# Not Obvious: Using cryptic function names or unclear logic
def file_read():
    ...

def write():
    ...
```


### Although that way may not be obvious at first unless you're Dutch.

The creator of python, Guido van Rossum: the "Benevolent Dictator For Life" (BDFL) of
the Python programming language.

![Photo of Guido van Rossum](https://upload.wikimedia.org/wikipedia/commons/2/21/Guido_van_Rossum_in_PyConUS24.jpg)

By <a href="//commons.wikimedia.org/wiki/User:Babaidas" title="User:Babaidas">Kushal Das</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/4.0" title="Creative Commons Attribution-Share Alike 4.0">CC BY-SA 4.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=148715324">Link</a>

### Now is better than never.

Don't procrastinate. Some say this is a reference to avoiding infinite loops and delayed execution,
but it's also just a good life lesson.

### Although never is often better than *right* now.

Another life lesson. Sometimes the best code is written after you've spent a few hours sitting
down and planning out what you're going to do. Don't rush into things.

**Why it Matters:** It's easy to write bad code quickly. It's much harder to write good code
quickly.

### If the implementation is hard to explain, it's a bad idea.

If you can't explain your code to someone else, it's probably too complex. A common technique is
called "Rubber Duck Debugging" - explaining your code to a rubber duck (or any inanimate object)
on your desk can often help you find issues or understand your code better.

### If the implementation is easy to explain, it may be a good idea.

Simple, straightforward code is often the best code.

### Namespaces are one honking great idea -- let's do more of those!

Namespaces are one of the most powerful features of Python. They allow you to organize your code
and avoid naming conflicts.

```
research_project/
├── research_project/
│   ├── main.py
│   ├── data/
│   │   ├── load_data.py
│   │   └── preprocess_data.py
│   ├── analysis/
│   │   ├── statistical_analysis.py
│   │   └── model_fitting.py
│   └── visualization/
│       ├── plot_results.py
│       └── generate_report.py
├── tests/
│   ├── test_load_data.py
│   └── test_preprocess_data.py
└── README.md
```

```python
# Importing functions from different modules using namespaces
from research_project.data.load_data import load_data
from research_project.analysis.model_fitting import fit_model
from research_project.visualization.plot_results import plot_results
```

**Why it Matters:** Namespaces help you organize your code and avoid naming conflicts. They make it
easier to understand where functions and classes come from and help prevent accidental overwriting
of variables or functions.

## Conclusion

The *Zen of Python* provides a set of guiding principles for writing clean, readable, and
maintainable code. They are by no means a strict set of rules, but rather a guideline for Python
developers to follow.
