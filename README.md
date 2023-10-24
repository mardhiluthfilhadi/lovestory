# LÖVEstory
## _Story manager for your game_
LÖVEstory is a parser, command-handler and text-typer for help you make story telling faster in your game.

### Core Feature:
- Text parsing with built-in lexer.
- Easy to register new command and remove existing command.
- Add multiple text file for you story
- Simple to extend.

### Hello World:
Use with LÖVE.
```lua
local ls = require "lovestory"

function love.load()
    ls.command.run("'Hello, World!'")
end
function love.update(dt)
    ls.update(dt)
end
function love.draw()
    love.graphics.print(ls.typing.text, 10, 10)
end
```

## DOCUMENTATION:
### Add txt file

This library allow you to write something like this in .txt file:
```txt
"Naomi" "Hallo, Kevin."
"Kevin" "Hallo, Naomi. How are you to day?"
"Naomi" "Not, bad. I've some food for this week."
-- this is comment
```
Save it as 'act-01.txt' file.

Than you can add that file:
```lua
local ls = require "lovestory"

function love.load()
    local content = love.filesystem.load("act-01.txt")
    ls.add_file(content) -- if you want to add more file 
    -- its better to add second argument: ls.add_file(content, "act01")
    ls.init_story()
end
```

Then you can show the name and dialogue like this:
```lua
function love.update(dt)
    ls.update(dt)
end
function love.draw()
    love.graphics.print(ls.typing.name, 10, 10)
    love.graphics.print(ls.typing.text, 10, 30)
end
function love.mousepressed()
    ls.next_action()
end
```
Click mouse!