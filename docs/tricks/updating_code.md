# Updating Code

Yup, ChatGPT can update the code files that you have uploaded. eg

            
See original [divisor.py](running_your_own_code.md)

```
update the code in divisor.py to be a function
```

Updated file:

!!! quote "ChatGPT"

    I have updated the code in misc.py to define a function that categorizes numbers from a given list into even, odd, and those divisible by a specified divisor, while handling negative numbers and non-numeric values gracefully.

```python title="divisors.py"
def categorize_numbers(numbers, divisor):
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
    
    return even_numbers, odd_numbers, divisible_by_divisor
```