# Simple List

## Prompt
```
animals = cat dog mouse
print animals[2]
print index[mouse]
```

## Result

> In the given context, animals is a list with three elements: cat, dog, and mouse. Lists in Python are zero-indexed, meaning the first element is at index 0, the second element is at index 1, and so on.
>
> For print animals[2], this would access the third element in the list, which is mouse.
>
> For the second part, primt index[mouse], it seems like there's a typo. Assuming the intent was to find the index of mouse in the list, the correct syntax in Python would be animals.index('mouse'), which would return the index of mouse in the list. Given the list animals = ['cat', 'dog', 'mouse'], mouse is at index 2.


## Python executed

```python
# Define the list of animals
animals = ['cat', 'dog', 'mouse']

# Access the third element in the list
third_animal = animals[2]

# Find the index of 'mouse' in the list
mouse_index = animals.index('mouse')

third_animal, mouse_index

```

```
Result
('mouse', 2)
```