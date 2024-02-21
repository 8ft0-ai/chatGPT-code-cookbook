# If within a loop

## Prompt

```
list = cat dog mouse

for item in list
   if there is a next item
     print item -> next item
   else
     print item -> STOP
```

## Python executed

```python
list = ['cat', 'dog', 'mouse']

for i in range(len(list)):
    if i < len(list) - 1:
        print(f"{list[i]} -> {list[i+1]}")
    else:
        print(f"{list[i]} -> STOP")
```

## Result

> This code iterates through each item in the list. If there is a next item, it prints the current item pointing to the next item (item -> next item). When it reaches the last item, since there is no next item, it prints item -> STOP.
> 
> Here's the expected output based on this logic:

```
cat -> dog
dog -> mouse
mouse -> STOP
```