# Looped Prompt

## Prompt
```
for subject in cat dog mouse
  write a poem as a [subject] and save it to poem-[subject].text

zip up all the files and provide a download link
```

## Python code executed

This results in a single execution (code run) that creates all the poems at one. This is fine for a simple task, but is each step is complex we could easily hit the 60 second limit on a single code run.

```python
from zipfile import ZipFile
import os

# Writing poems for cat, dog, and mouse and saving them to respective files
poems = {
    'cat': """
    In twilight's glow, I softly tread,
    A whisper in the night, unseen, unheard,
    With eyes like orbs that pierce the dark,
    I roam my kingdom, leave my mark.
    
    In silence, I watch the world below,
    Secrets of the night, only I know,
    On velvet paws, I glide, I roam,
    Under starlit skies, this earth my home.
    """,
    'dog': """
    With boundless joy, I greet the day,
    With wagging tail, I'm on my way,
    Through fields and streams, I leap and run,
    Underneath the shining sun.
    
    A loyal friend, always by your side,
    In every adventure, a faithful guide,
    With every bark, a story to tell,
    In every sniff, a world to spell.
    """,
    'mouse': """
    In hidden corners, I make my way,
    A tiny explorer, in night and day,
    Through walls and floors, I quietly sneak,
    A world of giants, strong but meek.
    
    With tiny treasures, I build my nest,
    In quiet moments, I find my rest,
    A small witness to the vast unknown,
    In secret spaces, I've grown.
    """
}

# Paths for saved poems and zip file
file_paths = []
zip_path = '/mnt/data/poems_subjects.zip'

# Save each poem to a text file
for subject, poem in poems.items():
    file_path = f'/mnt/data/poem-{subject}.txt'
    with open(file_path, 'w') as file:
        file.write(poem.strip())
    file_paths.append(file_path)

# Zip the poem files
with ZipFile(zip_path, 'w') as zipf:
    for file_path in file_paths:
        zipf.write(file_path, os.path.basename(file_path))

zip_path


```

## Notes

I asked ChatGPT to suggest a better initial prompt. It came back with a very verbose ....


> Write poems from the perspectives of a cat, a dog, and a mouse, highlighting their unique viewpoints and experiences. Each poem should encapsulate the essence of its subject's world, their joys, challenges, and the beauty they find in their existence. Save each poem in a separate text file named according to the subject (e.g., poem-cat.txt, poem-dog.txt, poem-mouse.txt). After writing all three poems, compress these files into a single ZIP archive for easy download. Ensure the process is streamlined and the poems reflect a deep understanding and imaginative insight into the lives of these animals.
