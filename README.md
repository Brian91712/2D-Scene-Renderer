# 2D Scene Renderer
This is a very simple and easy to use 2D Scene Renderer programmed using the Skript interpreted language created by the SkriptLang team.
## Dependencies
- Skript-2.15+
- oopsk-1.0-beta2
## Install
With [pacskage](https://github.com/miberss/pacskage):
```
/package install https://github.com/Brian91712/2D-Scene-Renderer
```
## Usage
To create a new scene, use `setup_scene(Scene struct)`, and fill in the details for `position`. The orientation of the scene is calculated using the yaw and pitch of the `position` location object. However, if you wish to provide a vector instead, you can set `forward` to your desired vector. You can additionally change the scale of the scene by modifying `scene_scale`, where the scale is blocks, and to make the scene generate a background, set `background_colour` using `rgb(r, g, b, a)`. For example:
```applescript
set {_scene} to setup_scene(Scene struct instance):
  position: location(0.5, 3, 0.5, world "world") # location
  forward: vector(1, 0, 0) # vector
  scene_scale: vector(5, 5, 0) # vector
  background_colour: rgb(0, 0, 0, 255) # colour
# This produces a scene facing the positive X direction with a scale of 5x5 blocks, and automatically generates a black background.
```
After creating our scene, you will find that it is empty. You can add elements to the scene using the `add_element_to_scene(Scene struct, Element struct)` function, and filling in the following details: `position`, `rotation`, `pivot`, `scale`, `colour`, and `interpolation`. `rotation` is in Euler Angles, and `interpolation` is the interpolation duration given to the text display entity representing this element. For example:
```applescript
set {_element} to add_element_to_scene({_scene}, Element struct instance):
  position: vector(0, 0, 0) # vector, scaled to 'scene screen pixels'
  rotation: vector(45, 0, 0) # vector, Euler Angles in degrees
  pivot: vector(0, 1, 0) # vector, in local scale. As in, 1 is the edge of the element, 0 is the center.
  scale: vector(20, 100, 0) # vector, scaled to 'scene screen pixels'.
  colour: rgb(255, 0, 0, 255) # colour
  interpolation: 1 tick # timespan
```
Make sure to save a reference to both the scene and the element. Otherwise, you will be incapable of modifying them later on. Anyway, now that we have an element on our scene, we can render the scene using the function `render_scene(Scene struct)`.
