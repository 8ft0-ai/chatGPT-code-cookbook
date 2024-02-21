# Linear Chain

If you ask ChatGPT to process items in the list, it will try and do them all within a single code run. A code run has a max duration of 60 seconds after which it will expire and terminate. This may be fine if your list is small but if you have time consuming actions or a long list, you are likely to hit this cut-off.

One way to get around this is to try and get ChatGPT to process each iteration as a seperate code run. I've not found a simple way to do this and ChatGPT tends to ignore any requests to process iterations sperately. see [Problem Space](#problem-space)

## Prompt

**Set Up**

``` title="Prompt"
mkdir steps poems

list = cat dog mouse

for item in items
   this = "STEP: {item} - write a poem about {item} and save it to poems/{item}.txt"
   next = "STOP"
   if there is a next item
     next = "  NEXT:  read the contents from  steps/{next item}.txt and perform the actions"
   print this > steps/{item} .txt
   print next >> steps/{item} .txt
```

```python title="ChatGPT Python"
# We need to generate instructions based on the provided template for each item in the new list of items.
# These instructions will be saved to files in the format specified.

items = ["cat", "dog", "mouse"]

# Iterate through the items list to create and save the instructions for each item
for index, item in enumerate(items):
    # Determine the 'next' action based on the position of the current item in the list
    if index + 1 < len(items):  # If there is a next item
        next_item = items[index + 1]
        next_action = f"  NEXT:  read the contents from  steps/{next_item}.txt and perform the actions"
    else:  # If this is the last item
        next_action = "STOP"
    
    # Format the instructions
    this_instruction = f"STEP: {item} - write a poem about {item} and save it to poems/{item}.txt"
    next_instruction = next_action
    
    # Define the filename for the current item's instructions
    filename = f"/mnt/data/steps/{item}.txt"
    
    # Save the instructions to a file
    with open(filename, "w") as file:
        file.write(this_instruction + "\n")
        file.write(next_instruction + "\n")

# Confirm the instructions have been created for the items as an example
example_steps_filenames = [f"steps/{item}.txt" for item in items]
example_steps_filenames

```
``` title="Prompt: List Files"
for item in list
  display the contents of steps/{item}.txt
```

```python title="ChatGPT Python"
# Reading and displaying the contents of steps/{item}.txt for each item in the list
step_contents = {}
for item in items:
    file_path = f'/mnt/data/steps/{item}.txt'
    with open(file_path, 'r') as file:
        step_contents[item] = file.read()

step_contents

```

```title="output"
{'cat': 'STEP: cat - write a poem about cat\nNEXT: read the contents from step-dog.txt and perform the actions',
 'dog': 'STEP: dog - write a poem about dog\nNEXT: read the contents from step-mouse.txt and perform the actions',
 'mouse': 'STEP: mouse - write a poem about mouse\nSTOP'}
```

**File Contents**
``` title="cat.txt"
STEP: cat - write a poem about cat and save it to poems/cat.txt
  NEXT:  read the contents from steps/dog.txt and perform the actions
```

``` title="dog.txt"
STEP: dog - write a poem about dog and save it to poems/dog.txt
  NEXT:  read the contents from steps/mouse.txt and perform the actions
```

``` title="mounse.txt"
STEP: mouse - write a poem about mouse and save it to poems/mouse.txt
STOP
```

## Kick off the Chain
``` title="Prompt"
read the contents from step/cat.txt and perform the actions 
```


```python title="ChatGPT Python"

# First, let's read the contents from the specified file to understand the actions required.
filename = "/mnt/data/steps/cat.txt"

# Read the file contents
with open(filename, "r") as file:
    instructions = file.read()

# Display the instructions to decide on the next steps
instructions

---
'STEP: cat - write a poem about cat and save it to poems/cat.txt\n  NEXT:  read the contents from  steps/dog.txt and perform the actions\n'

```

> The contents of steps/cat.txt instruct to:
>
> Write a poem about a cat and save it to poems/cat.txt.\
> Next, read the contents from steps/dog.txt and perform the actions.\
> Let's start by writing a poem about a cat and saving it as instructed.



``` title="Cat Poem"
In the heart of night, ...
```
> Now, I will save this poem to poems/cat.txt as instructed. ​​

```python title="ChatGPT Python"
# Define the poem for the cat
cat_poem = """
In the heart of night, under the moon's soft glow,
Lies a creature of stealth, moving silent and slow.
Eyes like lanterns, aglow with a mysterious light,
A cat on the prowl, a shadowy figure in the night.
"""

# Save the poem to the specified file
poem_filename = "/mnt/data/poems/cat.txt"

with open(poem_filename, "w") as file:
    file.write(cat_poem.strip())

poem_filename

```
> The poem about the cat has been successfully written and saved to poems/cat.txt.  
If you would like to view or download the poem, please let me know!  
Next, as per the instructions, I should read the contents from steps/dog.txt and perform the actions specified there.  
Would you like me to proceed with this next step?

You're going to have to prompt to move on to the next step.


---
## Problem Space

Let's try and write a set of poems
```title="Prompt"
list = cat dog mouse

for item in list
   write a poem about {item} and save it to poem-{item}.txt
```
ChatGPT does this in a single code run
```python title="ChatGPT Python"
# To address the user's request, we'll first define the poems for each item in the list,
# then save each poem to a file with the specified format.

# Define the list and poems
items = ["cat", "dog", "mouse"]
poems = {
    "cat": "In shadows sleek and silent paws tread,\nWhiskers twitch, under moonlight's spread.\nEyes aglow, a mystical sight,\nA silent whisper in the night.\nGraceful, with a velvet touch,\nIn its gaze, worlds unravel, much.\nMystery cloaked in fur so fine,\nA creature of magic, feline divine.",
    "dog": "Loyal companion, guardian true,\nEyes filled with love, through and through.\nTail wagging in endless glee,\nA friend for all, a key to glee.\nBrave and bold, through storm and sun,\nA heart of gold, second to none.\nIn fields of green, we run and play,\nTogether, we make the best of each day.",
    "mouse": "Tiny feet, swift and light,\nThrough the night, a quiet flight.\nClever and quick, with curious eyes,\nIn the moonlight, a small surprise.\nA world unseen, on silent paws,\nLiving by nature's unwritten laws.\nAmongst the stars, a dance so fine,\nA tiny heart, a brave design."
}

# Iterate through the list and save each poem to a file
for item in items:
    # Format the filename as requested
    filename = f"/mnt/data/poem-{item}.txt"
    # Write the poem to the specified file
    with open(filename, "w") as file:
        file.write(poems[item])

# Return the filenames to confirm the files were created
filenames = [f"poem-{item}.txt" for item in items]
filenames

```

> The poems for each item have been successfully created and saved to the specified files. Here are the filenames:
> 
> - poem-cat.txt
> - poem-dog.txt
> - poem-mouse.txt

This is clever. But what happens if we want a lot of poems ? say 100.

```python
items = [
    "apple", "ball", "car", "dog", "elephant", "flower", "guitar", "hat", "ice cream", 
    "jacket", "kite", "lamp", "moon", "notebook", "orange", "piano", "quilt", "robot", 
    "sunflower", "tree", "umbrella", "violin", "watch", "xylophone", "yacht", "zebra",
    "book", "cat", "duck", "earrings", "fish", "globe", "helicopter", "island", "jewel",
    "kangaroo", "lemon", "mango", "nest", "octopus", "pumpkin", "queen", "ring", "star",
    "turtle", "unicorn", "vase", "windmill", "x-ray", "yo-yo", "zipper", "cloud", "diamond",
    "egg", "flute", "grape", "house", "iceberg", "juice", "key", "lion", "mountain", "needle",
    "owl", "penguin", "quokka", "rabbit", "snake", "telescope", "violet", "wolf", "xenops",
    "yellow", "zeppelin", "acorn", "bridge", "candle", "desert", "eagle", "fountain", "giraffe",
    "harbor", "igloo", "jaguar", "koala", "lighthouse", "mushroom", "night", "ocean", "pear",
    "quartz", "rose", "shark", "tiger", "urchin", "volcano", "whale", "xerus", "yak", "zucchini"
]
```

```python title="ChatGPT Python"
# Given the new list of 100 random items, we'll create a basic poem for each item
# and save it to a file with the format "poem-{item}.txt".

# Since the list is large, we'll use a simple template for the poems to ensure uniqueness
# and manageability.
```

There is simply too much to do in a single step
