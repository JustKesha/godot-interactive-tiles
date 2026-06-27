# 🕹️ Godot 3D - Interactive Tiles
Modular base for a first-person Godot 3D game with customizable interactive tiles and unique inventory mechanics. 

*Feel free to use as a starting point for your project!*

> [!NOTE]
> There's a newer version avalible at - [godot-tile-game](https://github.com/JustKesha/godot-tile-game)<br>
> Which uses a different, cleaner approach to tile customization!

- [Contents](#includes)
- [Showcase](#simple-example)
- [Inventory](#inventory-system)
- [Quick start](#quick-start)

## Includes
- Interactive tiles system *- with fully customisable behaviors ([simple example](#interactions-showcase))*
- Unique inventory system - *with smooth animations ([details](#inventory-system))*
- Pixelation shader *- for easy retro visuals*
- Simple first-person controls
- Basic progression save system
- Clean signal-based code

## Simple Example
Here's a very basic example of what you can do with just one type of custom tile behavior, this tile will destroy any objects that activate it:

| GIF | Desc | Potential Uses |
|-|-|-|
| ![Activation](preview/one-cube.gif) | Object is dropped on a tile to activate it → gets destroyed by the tile's custom behavior script | "Lava" tiles that kill player unless they sacrifice an item |
| ![Queue activation](preview/multiple-cubes.gif) | Multiple objects destroyed one-by-one | Pressure plates that stay active while items remain, like a fire burning until out of fuel |
| ![Timed activation](preview/timer.gif) | Tile is held activated using a script → script stops → object on top is destroyed | Temporary bridges/gates that disappear/close after time |
| ![Forced activation](preview/set-to-pressed.gif) | Tile is forced into activated state via script → first object is removed → as a result, tile updates → item on top gets destroyed | Let the player choose to keep one of two bonus items / Create paths that close after the player walked on them (like one-way doors or no-retrace mazes) |

Script to achieve the shown tile behavior:
```js
extends Tile

func _on_just_pressed(object_pressing: Object) -> void:
	object_pressing.queue_free()
	$ActivationParticles.emitting = true
```

> [!NOTE]
> Tiles store references to all the objects on top of them (which you can use for custom behaviors). But by default only one object at a time is considered to be the one currently activating the tile. 

### Demo tiles
- Blue - no special effects
- Green - disappears after one use
- Yellow - saves the game
- Red - kills player & destroys items

## Inventory System
![Inventory system showcase](preview/inventory-showcase.gif)<br>
You can store items in inventory by:

1. Hovering & Clicking a hotkey
2. Drag & dropping them in

All items stored in inventory will slowly float in a circle above the player.<br>
As the player moves, the items will slowly follow them with a changeable delay.

You can hide inventory when its not active, to not abstract the sky view.<br>
And you can lower it when you need to look at your items.

> [!TIP]
> All 15 inventory parameters can be found & changed at the top of the `/scripts/player.gd` script.

### Demo controls
- E - collect
- Tab - show inventory
- R - toggle inventory
- Lmk - drag

## Why Use This?
- Already handles the annoying stuff (item management, save system)
- Clean signal-based architecture (means easy extension and custom behaviors)
- All core systems are implemented and tested
- Easy to reskin for your own game

## Quick Start
1. Clone this repository
2. Open in Godot 4.x (tested with 4.3)
3. Run `scenes/demo.tscn` to see the demo level

To create new tile types:
1. Duplicate any of existing tiles from `/objects/tiles/` or extend from the `/objects/tile.tscn`
2. Modify the assigned script to create custom behaviors (use signals provided by the parent object)

## License
MIT - use however you want (credit appreciated but not required)
