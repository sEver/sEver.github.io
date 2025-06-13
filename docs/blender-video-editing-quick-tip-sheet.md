# Blender Video Editing Quick Tip Sheet

## Loading the file and Initial setup
1. `File -> New -> Video Editing`
1. Drag a file onto the timeline

## Setting the size of the timeline
1. In side panel `Strip -> Time -> Start -> Set to 0` (for both audio and video strips)
1. `PgDn` to go to start of the strip, `Ctrl+Home` to set the beginning of render range
1. `PgUp` to go to end of the strip, `Ctrl+End` to set the end of render range
1. OR in Video Sequencer window go: `View -> Range -> Set Frame Range to Strips`
1. Rightclick video strip -> `Movie Strip -> Set Render Size` (sets output size to input size)
1. `Home` to zoom out to see entire strip within the window

## Editing
1. Play/Pause the video with `Space`
1. Move the header with a mouse to seek through the video faster
1. To cut the video at the header into two parts with `K` (strips have to be selected)
1. To delete unneeded parts - `Del`
1. On top of `Sequencer` window, click the magnet icon, to enable snapping
1. Move clips with mouse to snap them together, they snap well to the header as well
1. Snap selected strip contents to the current frame with `Shift+S`


## Setting the output format
1. Output tab (printer icon) 
    1. Make sure `Frame Rate` is `60fps`
    1. In `Output` section select the directory for output files
    1. Subsection `Encoding -> Video -> Output Quality` set to `Perceptually Lossless`

## Normalizing volume
1. Click the audio strip on the timeline
1. In side panel `Strip -> Sound -> Volume` grab the number with mouse and move right/left to raise/lower the volume, so the diagram in the strip is visible, but without the red cutoff markers

## Saving 
1. Press `Ctrl+F12` to render the video to output file
