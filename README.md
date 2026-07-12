# 2D Scene Renderer
This is a very simple and easy to use 2D Scene Renderer programmed using the Skript interpreted language created by the SkriptLang team.
## Dependencies
- Skript-2.15+
- oopsk-1.0-beta2
- skript-reflect v2.6.3+
## Install
With [pacskage](https://github.com/miberss/pacskage):
```
/package install https://github.com/Brian91712/2D-Scene-Renderer
```
## Usage
To create a new scene, use `setup_scene(Scene struct)`, and fill in the following details: `position`, `forward`, `scene_scale`, `background_colour`. If you don't set the `background_colour`, it will not generate a background. For example:
```applescript
set {_scene} to setup_scene(Scene struct instance):
  position: location(0.5, 3, 0.5, world "world") # location
  forward: vector(1, 0, 0) # vector
  scene_scale: vector(5, 5, 0) # vector
  background_colour: rgb(0, 0, 0, 255) # colour
# This produces a scene facing the positive X direction with a scale of 5x5 blocks, and
# automatically generates a black background.
```
After creating our scene, you will find that it is empty. You can add elements to the scene using the `add_element_to_scene(Scene struct, Element struct)` function, and filling in the following details: `position`, `rotation`, `pivot`, `scale`, `colour`, and `interpolation`. 

`rotation` is in Euler Angles (using radians.), and `interpolation` is the interpolation duration given to the text display entity representing this element. For example:
```applescript
set {_element} to add_element_to_scene({_scene}, Element struct instance):
  position: vector(0, 0, 0) # vector, scaled to 'scene screen pixels'
  rotation: vector(pi / 4, 0, 0) # vector, Euler Angles in radians
  pivot: vector(0, 1, 0) # vector, in local scale. As in, 1 is the edge of the element, 0 is the center.
  scale: vector(20, 100, 0) # vector, scaled to 'scene screen pixels'.
  colour: rgb(255, 0, 0, 255) # colour
  interpolation: 1 tick # timespan
```
Make sure to save a reference to both the scene and the element. Otherwise, you will be incapable of modifying them later on. Anyway, now that we have an element on our scene, we can render it using the function `render_element(Element struct, recalculate_orientation)`, where `recalculate_orientation` is a `boolean` that lets you decide whether the element's orientation is to be recalculated or not.

In addition, after making any changes to an element's variables, such as by setting its `position` or `rotation`, make sure to call the `update_element_all(Element struct)` or `update_element_position(Element struct, offset)` functions. For example:
```applescript
set {_element}->position to vector(10, 10, 0)
update_element_position({_element}, vector(10, 0, 0)) # Original position was vector(0, 10, 0), we moved it to vector(10, 10, 0), so the offset is vector(10, 0, 0)

set {_element}->position to vector(10, 0, 0)
update_element_all({_element}) # This function does not need you to provide an offset vector because it recalculates everything instead of just offsetting it. This is best used only if you change orientation, as otherwise it is not efficient to use.
```
However, it will not change visually until you run `render_element(Element struct, recalculate_orientation)`. Finally, if you don't want your scene anymore, you can delete it using the `delete_scene(Scene struct)` function, and delete individual elements with the `delete_element(Element struct)` function.
### Other useful functions:
`elements_overlap(Element struct, Element struct)`: Returns a boolean. Checks whether two elements overlap. This will return an incorrect value if you change an element and forget to update it, such as by changing its position.
`project_element(axis, Element struct)`: Returns a min and max. Projects an elements' corners onto an axis.
## Examples
`-examples/pong.sk`

https://github.com/user-attachments/assets/0d7419b0-3646-46a7-b7cb-842c5b1572fb

`Made by YouCanDream`

https://github.com/user-attachments/assets/aca31801-bd87-4045-a33f-c9fe3825f3da


