# Simple List

## Prompt
```
animals = cat dog mouse
print animals[2]
print index[mouse]
```

## Result

> In Python, to access the third element in a list called animals containing the elements cat, dog, and mouse, you would use animals[2], as list indices start at 0. To find the index of mouse in the list, you would use the .index() method, like animals.index('mouse'). Given the context, the third element is mouse, and the index of mouse in the list is 2


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