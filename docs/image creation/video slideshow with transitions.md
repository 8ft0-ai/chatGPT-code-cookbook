# Create a Video Slideshow with Transitions

This builds on from [creating multiple images](video%20slideshow.md) 



# Adding Video Transitions

Adding transitions requires a higher frames per second. This can result in the video creation taking longer than 60 seconds (this is the maximum time for a ChatGPT 'execution'). You'll need to experiment with fps settings and number of images in order to get the task to complete in under 60 seconds.

```
- make it 3 seconds per image
- add video transitions
- 6 frames per second
- use first 3 images only
```

# Result
<video width="480" height="640" controls>
  <source src="/chatGPT-code-cookbook/image%20creation/assets/video_slideshow_with_transitions.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>


---
# Under the hood
This is how ChatGPT handled the video slideshow creation


```python
from moviepy.editor import ImageClip, concatenate_videoclips, vfx

# Re-defining the paths to the first three images
image_paths = [
    "/mnt/data/A_detailed_portrait_of_a_cat,_looking_directly_at_.png",
    "/mnt/data/A_detailed_portrait_of_a_cat_in_a_playful_pose,_wi.png",
    "/mnt/data/A_serene_portrait_of_a_cat_sitting_by_a_window,_wi.png"
]

# Creating clips with 2 seconds duration each
clips = [ImageClip(path).set_duration(2) for path in image_paths]

# Applying fade in and fade out transitions for each clip
for i, clip in enumerate(clips):
    clips[i] = clip.fx(vfx.fadein, 1).fx(vfx.fadeout, 1)

# Concatenating the clips with crossfade transition
final_clip = concatenate_videoclips(clips, method="compose", padding=-1)

# Writing the video file with 2 seconds per image, transitions, and at 6 fps
output_path_with_transitions = "/mnt/data/cat_images_video_3imgs_2s_transitions_6fps.mp4"
final_clip.write_videofile(output_path_with_transitions, fps=6)

```