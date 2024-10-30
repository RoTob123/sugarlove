# sugarlove
An interface to use the SUGAR API with Love2D

[SUGAR](https://trasevol.dog/sugar/) is a retro-inspired, limitation-led C++ game engine!
It features a minimalist API and a retro graphics infrastructure for making authentic low-resolution games.
Sugarcoat is an attempt to reproduce most of SUGAR's behavior in [Love2D](https://love2d.org/).

**[Go to the documentation hub!](/doc/sugar.md#sugar)**

## Getting started
First of all, make sure the folder `sugarcoat` is in your project's folder and is complete.
Then do `require("sugarcoat/sugarcoat")` at the top of your `main.lua`.

 

Next, do one of two:
```lua
sugar.utils.using_package(sugar.S, true)
```

OR

```lua
sugar.utils.using_package(sugar, true)
local S = sugar.S
```

In both cases, instead of typing `sugar.<class>.foo()`, you can just do `S.foo()`!

 

Then you can simply use `love.load`, `love.update` and `love.draw` to make your game. Make sure to use `sugar.init_sugar(window_name, w, h, scale)` at the top of `love.load`. The rest of the sugar systems will automatically update around `love.update()`, `love.draw()`.

(you may change the screen stretching style with the various `sugar.gfx.screen_...` functions)

In case you do not intend to use `love.update()` and `love.draw()`, you should call `sugar.sugar_step()` to update the input and time subsystems, and `sugar.gfx.flip()` to render the screen.

 

And that is the essentials. I do recommend you at least skim through the rest of the manual to be aware of the various functions available to you.

Here is a very quick example showing some of the basics:

```lua
require("sugarcoat/sugarcoat")
sugar.utility.using_package(sugar.S, true)

local x = 64
local y = 64

function love.load()
  init_sugar("Hello world!", 128, 128, 3)
  
  set_frame_waiting(60)
  
  register_btn(0, 0, input_id("keyboard", "left"))
  register_btn(1, 0, input_id("keyboard", "right"))
  register_btn(2, 0, input_id("keyboard", "up"))
  register_btn(3, 0, input_id("keyboard", "down"))
end

function love.update()
  if btn(0) then x = x - 2 end
  if btn(1) then x = x + 2 end
  if btn(2) then y = y - 2 end
  if btn(3) then y = y + 2 end
end

function love.draw()
  cls()
  circfill(x, y, 4 + 2 * cos(t()), 3)
end
```

Check out **[chill_snake.lua](/chill_snake.lua)** for a much more complete example!