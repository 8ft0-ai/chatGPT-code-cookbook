# Running your own code

Upload a python file and have ChatGPT run it for you.

eg 

```python
# divisors.py

# Define a list of mixed data types including numbers and a string
numbers = [10, 15, 22, -5, 30, 45, 60]

# Set the divisor to 10 for divisibility check
divisor = 5

# Initialize lists to store categorized numbers
even_numbers = []
odd_numbers = []
divisible_by_divisor = []

# Loop through each item in the numbers list
for number in numbers:
    try:
        # Ignore negative numbers by continuing to the next iteration
        if number < 0:
            continue
        
        # Check if the number is even or odd and append to respective list
        if number % 2 == 0:
            even_numbers.append(number)
        else:
            odd_numbers.append(number)
            
        
        # Check if the number is divisible by the specified divisor
        if number % divisor == 0:
            divisible_by_divisor.append(number)
    except TypeError:
        # Handle non-numeric values gracefully
        print(f"Non-numeric value encountered: {number}")
        pass


print(f"Even numbers: {even_numbers}")
print(f"Odd numbers: {odd_numbers}")
print(f"Numbers divisible by {divisor}: {divisible_by_divisor}")
```

```
show only the results, in json format, of executing this script: divisors.py 
```

OUtput
```json
{
  "even_numbers": [10, 22, 30, 60],
  "odd_numbers": [15, 45],
  "divisible_by_divisor": [10, 15, 30, 45, 60]
}
```