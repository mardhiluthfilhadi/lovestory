#LÖVEstory
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

Click the mouse!

### Add new command
Command is short of function you call inside the story text file.

Structure of command is like this:
```txt
command_name <arg1> <arg2> ...
```

for example you can add command like this:
```lua
local ls = require "lovestory"

-- This command will print something to your console.
ls.command.register("print", function(text, text2)
    print(text, text2) -- this just example for multi argument
end)
```

now you can call print command like this:
```txt
print "This is print test!" " and is it Work?"
```
if it's needed you can passing argument in multiline with 'begin' and 'end' keywords after command name:
```txt
print begin
    "This is print test!"
    " and is it Work?"
end
```
or
```txt
print begin "This is print test!" 
    " and is it Work?"
end
```
or 

```txt
print begin

"This is print test!" " and is it Work?"
end
```
honestly indentation, spaces, newlines it doesn't matters.