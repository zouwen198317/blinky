# Blinky

<img src="readme-img/blinky.png" align="right" width="220px"/>

Blinky is a fisheye addon for the game, Quake.  Its purpose was to find a
__practical fisheye for gaming__, and we found one, the [Panini] lens!

[>> Watch the video](http://youtu.be/jQOJ3yCK8pI)

- continues the work of [Fisheye Quake](http://strlen.com/gfxengine/fisheyequake/)
- uses the cross-platform [TyrQuake engine](http://disenchant.net/tyrquake/)
- adds a Lua scripting environment for easy experimenting
- explores different ways to see 180º-360º around you

<img src="readme-img/old-way.png" width="360px"> <img src="readme-img/new-way.png" width="360px">


## Try it out

Please install [Lua](http://www.lua.org/) and [SDL2 dev libs](https://www.libsdl.org/download-2.0.php):

```sh
# Mac OSX
brew install lua
brew install sdl2

# Linux
sudo apt-get install lua
sudo apt-get install libsdl2-dev
```

Then build and play:

```sh
# Build blinky
./build.sh

# Play blinky by launching Quake demo
./play.sh
```

## Full list of commands

```sh
fisheye <0|1>     # enable/disable fisheye mode
f_help            # show quick start options
f_globe <name>    # choose a globe (affects picture quality and render speed)
f_lens <name>     # choose a lens (affects the shape of your view)
f_fov <degrees>   # zoom to a horizontal FOV
f_vfov <degrees>  # zoom to a vertical FOV
f_cover           # zoom in until screen is covered (some parts may be hidden)
f_contain         # zoom out until screen contains the entire image (if possible)
f_rubix           # display colored grid for each rendered view in the globe
f_saveglobe       # take screenshots of each globe face (environment map)
```

## Experiment Results

- Use Standard projection for FOV ≤ 110º.  Anything more leads to increasing distortion.
- Use Panini projection for FOV ≤ 200º.  Very practical, wide motion lens with low distortion.
- No preferences for FOV ≤ 360º.  They are more aesthetic than practical.

## How does it work?

View construction happens in two stages:

1. Capture surrounding pixels with multiple camera shots. (via __Globe__ script)
1. Stitch the shots together on the screen to get a hyper-wide FOV. (via __Lens__ script)

Your view can be customized by swapping each script out for another; choose
from several presets or even create your own.

__NOTE__: See the beginning of `NQ/fisheye.c` for extensive documentation and
diagrams describing the fisheye process in detail.


## Code Navigation

__NOTE__: See the beginning of `fisheye.c` for extensive documentation and
diagrams describing the fisheye process in detail.

If you wish to see the engine modifications that made this possible, see the
[engine patch](engine/fisheye.patch), generated by:

```
git diff 23119f4eb2ac6b5cef3e1ebfc785189b011aae26.. NQ common include Makefile
```

The meat of the work is done by the following files, which are completely
new additions to the engine:

- engine/NQ/fisheye.c
- engine/include/fisheye.h
- lua/lenses/*.lua
- lua/globes/*.lua

[Panini]: http://tksharpless.net/vedutismo/Pannini/
