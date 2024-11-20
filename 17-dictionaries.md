---
title: Dictionaries
teaching: 30
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain why keyed data objects exist.
- Write programs that store values in dictionaries, modify them, and iterate over them.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How is a dictionary different from a list?

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: instructor

Estimated: 10:00 - 10:45

:::::::::::::::::::::::::::::::::::::

## A dictionary stores values under keys.

- Sometimes we want to store pairs of related values
- A list of lists would be difficult to manage
- Use a *dictionary* to store values "keyed" by a unique value
  - Defined by curly braces `{...}`
  - *keys* and *values* are separated by a colon `:`
  - key/value pairs are separated by commas `,`
```python
inventory = {
    "apples": 12,
    "bananas": 4,
    "coconuts": 0
}
print('inventory:', inventory)
```

```output
apples: 12
items in inventory: 3
```

## Use a key to fetch the corresponding value from the dictionary

```python
print('number of apples:', inventory['apples'])
print('number of coconuts:', inventory['coconuts'])
```

```output
number of apples: 12
number of coconuts: 0
```

## A value can be replaced by assinging to it

```python
inventory['apples'] = 7
print('number of apples is now:', inventory['apples'])
```

```output
number of apples is now: 7
```

## Use a key to add a new value to a dictionary

```python
print('inventory is now:', inventory)
inventory["oranges"] = 24
print('inventory is now:', inventory)
```

```output
inventory is now: {'apples': 7, 'bananas': 4, 'coconuts': 0}
inventory is now: {'apples': 7, 'bananas': 4, 'coconuts': 0, 'oranges': 24}
```

## Use `del` to remove a key-value pair from a dictionary

- Use the `del` statement to remove a key-value pair from a dictionary

```python
del inventory['bananas']
print('inventory is now:', inventory)
```

```output
inventory is now: {'apples': 7, 'coconuts': 0, 'oranges': 24}
```

## Keys are unique

- If you assign a value to an existing key, it replaces the existing value

```python
inventory['oranges'] = 100
print('inventory is now:', inventory)
```

```output
inventory is now: {'apples': 7, 'coconuts': 0, 'oranges': 100}
```

## Dictionaries may contain values of different types

- There is no restriction on the types of values a dictionary may contain
- You can mix values in the same dictionary

```python
inventory['limes'] = "Out of Stock"
print('inventory is now', inventory)
```

```output
inventory is now: {'apples': 7, 'coconuts': 0, 'oranges': 100, 'limes': 'Out of Stock'}
```

## Requesting a key that doesn't exist is an error

- Python will report a `KeyError` if we attempt to access a key that doesn't exist

```python
print('number of pears:', inventory['pears'])
```

```output
KeyError: 'pears'
```

## We can check it a key exists before using it

- Use the `in` operator to check if a key exists in a dictionary

```python
print('inventory is now:', inventory)
print('is there a key for oranges?', 'oranges' in inventory)
print('is there a key for pears?', 'pears' in inventory)
```

```output
inventory is now: {'apples': 7, 'coconuts': 0, 'oranges': 100, 'limes': 'Out of Stock'}
is there a key for oranges? True
is there a key for pears? False
```

## We can get a list of all the keys / values in a dictionary

- Use the `.keys()` method to get a list of all the keys in a dictionary
- Use the `.values()` method to get a list of all the values in a dictionary
  - these methods return a "dict_keys" or "dict_values" object, which behave similarly to lists

```python
print("keys in inventory:", inventory.keys())
print("values in inventory:", inventory.values())
```

```output
keys in inventory: dict_keys(['apples', 'coconuts', 'oranges', 'limes'])
values in inventory: dict_values([7, 0, 100, 'Out of Stock'])
```


:::::::::::::::::::::::::::::::::::::::  challenge

## Fill in the Blanks

Fill in the blanks so that the program below produces the output shown.

```python
prices = {
    "laptop": ___,
    ______: ___,
    ______: 85,
}
print('all prices', prices)
print('price of mouse:', prices[______])
prices[______] = 50
print('all prices', prices)
```

```output
all prices {'laptop': 500, 'mouse': 10, 'camera': 85}
price of mouse: 10
all prices {'laptop': 500, 'mouse': 10, 'camera': 85, 'printer': 50}
```

:::::::::::::::  solution

## Solution

```python
prices = {
    "laptop": 500,
    "mouse": 10,
    "camera": 85
}
print('all prices', prices)
print('price of mouse:', prices['mouse'])
prices["printer"] = 50
print('all prices', prices)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Adding Two Values

Given the following dictionary, how would we get the cost of a laptop and a camera?

```python
prices = {
    "laptop": 500,
    "mouse": 10,
    "camera": 85
}
```

```output
price of a laptop + camera: 585
```

:::::::::::::::  solution

## Solution

```python
prices = {
    "laptop": 500,
    "mouse": 10,
    "camera": 85
}
print('price of a laptop + camera:', prices['laptop'] + prices['camera'])
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Summing Values

Given the following dictionary, how could we calculate the total cost of all items?

Hint: try the *sum* function

```python
prices = {
    "laptop": 500,
    "mouse": 10,
    "camera": 85,
    "printer": 50
}
```

```output
total cost: 645
```

:::::::::::::::  solution

```python

prices = {
    "laptop": 500,
    "mouse": 10,
    "camera": 85,
    "printer": 50
}

print('total cost:', sum(prices.values()))
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::
