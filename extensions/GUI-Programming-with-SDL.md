---
layout: page
lang: en
title: GUI Programming with SDL
---

GUI Programming with SDL
------------------------

Gura provides a module named `sdl` that uses [SDL](http://www.libsdl.org/) library.

SDL, Simple DirectMedia Layer, is a cross-platform development library
designed to provide low level access to audio, keyboard, mouse, joystick,
and graphics hardware via OpenGL and Direct3D.

### Simple Example

The following script only shows a blank window by using SDL.

    import(sdl)
    
    sdl.Init(sdl.INIT_EVERYTHING)
    screen = sdl.SetVideoMode(640, 480, 16, sdl.SWSURFACE)
    repeat {
        event = sdl.WaitEvent()
        (event.type == sdl.QUIT) && break
    }

At first, you have to initialize SDL's status by calling `sdl.Init`.
Then, calling `sdl.SetVideoMode` with screen size and depth in its arguments
will show a window.

Unlike other GUI platform, SDL requires you to implement an event handling loop explicitly.
The function `sdl.WaitEvent` would wait until some events come in
and returns an instance of `sdl.Event` class that contains event type and related information.

### More Sample Scripts

You can find sample scripts using SDL on
[GitHub repository](https://github.com/gura-lang/gura/tree/master/sample/sdl/).
