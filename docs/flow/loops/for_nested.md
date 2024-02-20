# Nested

## Prompt

```
for outer in 0-2  
  for inner in A B C
    print outer-inner
```
## Python code executed

```python
# Generating the requested pattern with nested loops

pattern = []
for outer in range(3):  # Loop through numbers 0 to 2
    for inner in ['A', 'B', 'C']:  # Loop through letters A to C
        pattern.append(f"{outer}-{inner}")

pattern_output = "\n".join(pattern)
pattern_output

```

## Results
```
0-A
0-B
0-C
1-A
1-B
1-C
2-A
2-B
2-C
```
