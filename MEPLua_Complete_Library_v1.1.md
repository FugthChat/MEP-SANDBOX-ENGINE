# MEPLua Complete Library v1.1
## Micah Engine Programming Language - Comprehensive Reference

**Version:** 1.1.0  
**Engine:** Micah Engine Studio  
**Date:** December 2025

---

# TABLE OF CONTENTS

1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [Core Concepts](#core-concepts)
4. [Script Lifecycle](#script-lifecycle)
5. [Instance System](#instance-system)
6. [Properties Reference](#properties-reference)
7. [Events System](#events-system)
8. [Math & Data Types](#math-data-types)
9. [Gameplay Tutorials](#gameplay-tutorials)
10. [Character Rigging](#character-rigging)
11. [Complete API Reference](#api-reference)
12. [Example Projects](#example-projects)

---

# 1. INTRODUCTION

MEPLua is the scripting language for Micah Engine Studio, inspired by Roblox Lua but designed for professional game development. This manual covers everything from basic scripts to advanced gameplay systems.

## What You'll Learn

- ✅ Writing your first script
- ✅ Creating interactive gameplay
- ✅ Building tycoon systems
- ✅ Character rigging and animation
- ✅ Event-driven programming
- ✅ Complete API reference

---

# 2. GETTING STARTED

## Your First Script

1. **Create a Part**: Right-click Workspace → Insert Object → Parts → Part
2. **Add a Script**: Right-click the Part → Insert Object → Scripting → Script
3. **Open the Script**: Double-click the Script in Explorer
4. **Write Code**:

```lua
-- My first MEPLua script!
function on_start()
    print("Hello from Micah Engine!")
    print("Parent object: " .. script.Parent.Name)
end
```

5. **Run**: Click Play ▶️ in the toolbar
6. **Check Output**: Look at the Output panel at the bottom

## Script Locations

Scripts can be placed:
- **Inside Parts** - Affect that specific part
- **Inside Models** - Control the entire model
- **In Workspace** - Global game logic

---

# 3. CORE CONCEPTS

## The Script Object

Every script has access to:

```lua
script          -- The script object itself
script.Parent   -- The object containing this script
workspace       -- The root game world
```

## Variables

```lua
-- Local variables (recommended)
local myNumber = 42
local myString = "Hello"
local myBool = true

-- Global variables (use sparingly)
globalCounter = 0
```

## Functions

```lua
-- Define a function
function myFunction(param1, param2)
    print("Parameters: ", param1, param2)
    return param1 + param2
end

-- Call a function
local result = myFunction(5, 10)  -- Returns 15
```

---

# 4. SCRIPT LIFECYCLE

MEPLua scripts have two main callback functions:

## on_start()

Called **once** when you press Play. Use for initialization:

```lua
function on_start()
    print("Game started!")
    
    -- Initialize variables
    local part = script.Parent
    part.Color = Color3.new(1, 0, 0)  -- Make it red
    
    -- Connect events
    part.Touched:Connect(onTouched)
end
```

## on_update(dt)

Called **every frame** (~60 times per second). `dt` = delta time (seconds since last frame):

```lua
local rotation = 0

function on_update(dt)
    -- Rotate the part
    rotation = rotation + (90 * dt)  -- 90 degrees per second
    script.Parent.Rotation = Vector3.new(0, rotation, 0)
end
```

## Complete Example

```lua
-- Spinning, Color-Changing Part
local part = script.Parent
local rotation = 0
local colorTimer = 0

function on_start()
    print("Initialized spinning part: " .. part.Name)
end

function on_update(dt)
    -- Spin
    rotation = rotation + (45 * dt)
    part.Rotation = Vector3.new(0, rotation, 0)
    
    -- Change color every second
    colorTimer = colorTimer + dt
    if colorTimer >= 1 then
        colorTimer = 0
        part.Color = Color3.fromRGB(
            math.random(0, 255),
            math.random(0, 255),
            math.random(0, 255)
        )
    end
end
```

---

# 5. INSTANCE SYSTEM

## Creating Objects

Use `Instance.new()` to create objects at runtime:

```lua
function on_start()
    -- Create a new part
    local newPart = Instance.new("Part")
    newPart.Name = "DynamicPart"
    newPart.Position = Vector3.new(0, 10, 0)
    newPart.Size = Vector3.new(2, 2, 2)
    newPart.Color = Color3.fromRGB(100, 200, 255)
    newPart.Parent = workspace  -- Add to world
    
    print("Created part at", newPart.Position)
end
```

## Available Instance Types

### Parts & Shapes
- `Part` - Standard cube
- `Sphere` - Spherical part
- `Cylinder` - Cylindrical part
- `WedgePart` - Wedge/ramp shape
- `CornerWedgePart` - Corner wedge
- `MeshPart` - Custom mesh

### Gameplay Objects
- `Model` - Container for multiple parts
- `Humanoid` - Character controller
- `Tool` - Equippable item
- `SpawnLocation` - Player spawn point

### Scripting
- `Script` - Server script
- `LocalScript` - Client script
- `ModuleScript` - Reusable code module

### Physics & Forces
- `BodyVelocity` - Apply velocity
- `BodyPosition` - Move to position
- `BodyGyro` - Control rotation
- `Explosion` - Create explosion

### Rigging
- `Motor6D` - Animated joint
- `Weld` - Fixed joint
- `Attachment` - Connection point

### Values (Data Storage)
- `BoolValue` - Store boolean
- `IntValue` - Store integer
- `NumberValue` - Store number
- `StringValue` - Store string
- `Vector3Value` - Store Vector3
- `ObjectValue` - Store object reference

### Audio & Visual
- `Sound` - Play audio
- `Decal` - Surface image
- `Texture` - Repeating surface image
- `Camera` - View camera

---

# 6. PROPERTIES REFERENCE

## BasePart Properties

All parts (Part, Sphere, Cylinder, etc.) have these properties:

### Transform
```lua
part.Position = Vector3.new(x, y, z)    -- World position
part.Rotation = Vector3.new(rx, ry, rz) -- Euler angles (degrees)
part.Size = Vector3.new(sx, sy, sz)     -- Dimensions
part.Scale = Vector3.new(1, 1, 1)       -- Scale multiplier
```

### Appearance
```lua
part.Color = Color3.new(r, g, b)           -- RGB 0-1
part.Color = Color3.fromRGB(r, g, b)       -- RGB 0-255
part.Transparency = 0.5                     -- 0=opaque, 1=invisible
part.Reflectance = 0.3                      -- 0-1 shininess
part.Material = "Plastic"                   -- Material type
```

### Physics
```lua
part.Anchored = true                        -- Fixed in place
part.CanCollide = true                      -- Solid to other parts
part.Velocity = Vector3.new(vx, vy, vz)    -- Current velocity
part.Mass = 10.0                            -- Mass in studs³
```

### State
```lua
part.Name = "MyPart"                        -- Object name
part.Locked = false                         -- Lock in studio
part.Visible = true                         -- Visibility
```

## Humanoid Properties

Character controller properties:

```lua
humanoid.Health = 100                       -- Current HP
humanoid.MaxHealth = 100                    -- Maximum HP
humanoid.WalkSpeed = 16                     -- Studs per second
humanoid.JumpPower = 50                     -- Jump strength
humanoid.AutoRotate = true                  -- Auto-face movement
humanoid.PlatformStand = false              -- Ragdoll state
```

## Model Properties

Container properties:

```lua
model.PrimaryPart = model.Head              -- Main part
model.Name = "Character"                    -- Model name

-- Model also has Position, Rotation, Scale
-- These affect ALL children relatively
model.Position = Vector3.new(0, 5, 0)       -- Move entire model
```

---

# 7. EVENTS SYSTEM

Events let you react to gameplay actions.

## Connecting to Events

```lua
function on_start()
    local part = script.Parent
    
    -- Connect event to function
    part.Touched:Connect(function(otherPart)
        print(part.Name .. " was touched by " .. otherPart.Name)
    end)
end
```

## Common Events

### Part.Touched
Fires when another part touches this part:

```lua
part.Touched:Connect(function(otherPart)
    -- Check if it's a character
    local humanoid = otherPart.Parent:FindFirstChild("Humanoid")
    if humanoid then
        print("Character touched!")
        humanoid.Health = humanoid.Health - 10
    end
end)
```

### Humanoid.Died
Fires when humanoid health reaches 0:

```lua
humanoid.Died:Connect(function()
    print(humanoid.Parent.Name .. " died!")
    -- Respawn logic here
end)
```

### Humanoid.HealthChanged
Fires whenever health changes:

```lua
humanoid.HealthChanged:Connect(function(newHealth)
    print("Health: " .. newHealth .. "/" .. humanoid.MaxHealth)
    
    if newHealth < 20 then
        print("Low health warning!")
    end
end)
```

---

# 8. MATH & DATA TYPES

## Vector3

3D position/direction/size:

```lua
-- Create
local vec = Vector3.new(10, 5, -3)

-- Access components
print(vec.X, vec.Y, vec.Z)  -- 10, 5, -3

-- Math operations
local v1 = Vector3.new(1, 0, 0)
local v2 = Vector3.new(0, 1, 0)
local sum = v1 + v2                    -- (1, 1, 0)
local scaled = v1 * 5                  -- (5, 0, 0)

-- Properties
print(vec.Magnitude)                   -- Length: ~11.6
print(vec.Unit)                        -- Normalized direction

-- Common vectors
local up = Vector3.new(0, 1, 0)
local forward = Vector3.new(0, 0, -1)
local right = Vector3.new(1, 0, 0)
```

## Color3

RGB color:

```lua
-- Create (0-1 range)
local red = Color3.new(1, 0, 0)

-- Create from 0-255 range
local blue = Color3.fromRGB(0, 0, 255)
local purple = Color3.fromRGB(128, 0, 255)

-- Create from HSV (Hue, Saturation, Value)
local hue = 0.5      -- Cyan at 0.5
local rainbow = Color3.fromHSV(hue, 1, 1)

-- Access components
print(red.R, red.G, red.B)  -- 1, 0, 0
```

## Math Functions

```lua
-- Random
math.random()              -- Random 0-1
math.random(10)            -- Random 1-10
math.random(5, 15)         -- Random 5-15

-- Rounding
math.floor(3.7)            -- 3
math.ceil(3.2)             -- 4
math.round(3.5)            -- 4

-- Trigonometry (radians)
math.sin(angle)
math.cos(angle)
math.tan(angle)
math.deg(radians)          -- Convert to degrees
math.rad(degrees)          -- Convert to radians

-- Other
math.abs(-5)               -- 5
math.sqrt(16)              -- 4
math.pow(2, 8)             -- 256
math.min(3, 7, 2)          -- 2
math.max(3, 7, 2)          -- 7
```

---

# 9. GAMEPLAY TUTORIALS

## Kill Brick

Classic instant-death obstacle:

```lua
-- Place in a Part colored red
local killBrick = script.Parent

function on_start()
    killBrick.Touched:Connect(onTouched)
    print("Kill brick active!")
end

function onTouched(hit)
    -- Find humanoid in parent
    local humanoid = hit.Parent:FindFirstChild("Humanoid")
    
    if humanoid then
        humanoid.Health = 0  -- Instant kill
        print(hit.Parent.Name .. " touched kill brick!")
    end
end
```

## Damage Zone

Continuous damage over time:

```lua
local damageZone = script.Parent
local damagePerSecond = 25
local playersInZone = {}

function on_start()
    -- Track when players enter
    damageZone.Touched:Connect(function(hit)
        local humanoid = hit.Parent:FindFirstChild("Humanoid")
        if humanoid and not playersInZone[humanoid] then
            playersInZone[humanoid] = true
            print(hit.Parent.Name .. " entered damage zone")
        end
    end)
    
    -- Track when players leave
    damageZone.TouchEnded:Connect(function(hit)
        local humanoid = hit.Parent:FindFirstChild("Humanoid")
        if humanoid then
            playersInZone[humanoid] = nil
            print(hit.Parent.Name .. " left damage zone")
        end
    end)
end

function on_update(dt)
    -- Damage all players in zone
    for humanoid, _ in pairs(playersInZone) do
        if humanoid.Health > 0 then
            humanoid.Health = humanoid.Health - (damagePerSecond * dt)
        else
            playersInZone[humanoid] = nil
        end
    end
end
```

## Healing Zone

Restore health over time:

```lua
local healZone = script.Parent
local healPerSecond = 20

function on_start()
    healZone.Color = Color3.fromRGB(0, 255, 100)  -- Green for healing
    healZone.Touched:Connect(onTouched)
end

function onTouched(hit)
    local humanoid = hit.Parent:FindFirstChild("Humanoid")
    
    if humanoid and humanoid.Health < humanoid.MaxHealth then
        -- Heal but don't exceed max
        humanoid.Health = math.min(
            humanoid.Health + healPerSecond,
            humanoid.MaxHealth
        )
    end
end
```

## Teleporter

Transport between two locations:

```lua
-- Place in the entrance pad
local entrance = script.Parent
local exitPosition = Vector3.new(50, 5, 50)  -- Destination

function on_start()
    entrance.Color = Color3.fromRGB(255, 200, 0)
    entrance.Touched:Connect(onTouched)
end

function onTouched(hit)
    -- Teleport the root part of the character
    if hit.Parent:FindFirstChild("HumanoidRootPart") then
        local rootPart = hit.Parent.HumanoidRootPart
        rootPart.Position = exitPosition
        print("Teleported " .. hit.Parent.Name)
    end
end
```

---

# 10. TYCOON SYSTEMS

## Part Dropper

Spawn parts at intervals:

```lua
local dropper = script.Parent
local dropRate = 2          -- Seconds between drops
local dropValue = 10        -- Value of each part
local timer = 0

function on_start()
    print("Dropper ready: " .. dropper.Name)
end

function on_update(dt)
    timer = timer + dt
    
    if timer >= dropRate then
        timer = 0
        spawnPart()
    end
end

function spawnPart()
    local part = Instance.new("Part")
    part.Name = "DroppedPart"
    part.Size = Vector3.new(1, 1, 1)
    part.Color = Color3.fromRGB(255, 215, 0)  -- Gold
    part.Position = Vector3.new(
        dropper.Position.X,
        dropper.Position.Y - 2,
        dropper.Position.Z
    )
    
    -- Store value in part
    local valueTag = Instance.new("IntValue")
    valueTag.Name = "Value"
    valueTag.Value = dropValue
    valueTag.Parent = part
    
    part.Parent = workspace
    print("Dropped part worth $" .. dropValue)
end
```

## Conveyor Belt

Move parts along a path:

```lua
local conveyor = script.Parent
local moveSpeed = 5         -- Studs per second
local direction = Vector3.new(1, 0, 0)  -- Move along X axis

function on_start()
    conveyor.Color = Color3.fromRGB(100, 100, 100)
end

function on_update(dt)
    -- Find all parts touching the conveyor
    local parts = workspace:GetChildren()
    for _, part in ipairs(parts) do
        if part:IsA("BasePart") and isTouching(conveyor, part) then
            movePart(part, dt)
        end
    end
end

function movePart(part, dt)
    local movement = direction * moveSpeed * dt
    part.Position = part.Position + movement
end

function isTouching(part1, part2)
    -- Simple distance check
    local distance = (part1.Position - part2.Position).Magnitude
    local combinedSize = (part1.Size + part2.Size).Magnitude / 2
    return distance < combinedSize
end
```

## Collector

Collect parts and award money:

```lua
local collector = script.Parent
local playerMoney = 0

function on_start()
    collector.Color = Color3.fromRGB(0, 255, 0)
    collector.Touched:Connect(onTouched)
    print("Collector ready!")
end

function onTouched(hit)
    -- Only collect dropped parts
    if hit.Name == "DroppedPart" then
        local valueTag = hit:FindFirstChild("Value")
        
        if valueTag then
            playerMoney = playerMoney + valueTag.Value
            print("Collected! Total money: $" .. playerMoney)
            
            -- Destroy the part
            hit:Destroy()
        end
    end
end
```

## Complete Tycoon System

Combine all three:

```lua
-- Main Tycoon Controller
local tycoonData = {
    money = 0,
    droppers = {},
    conveyors = {},
    collectors = {}
}

function on_start()
    setupTycoon()
    print("Tycoon initialized!")
end

function setupTycoon()
    -- Setup dropper
    local dropper = workspace:FindFirstChild("Dropper1")
    if dropper then
        tycoonData.droppers["Dropper1"] = {
            part = dropper,
            rate = 2,
            value = 10,
            timer = 0
        }
    end
    
    -- Setup collector
    local collector = workspace:FindFirstChild("Collector1")
    if collector then
        collector.Touched:Connect(function(hit)
            collectPart(hit)
        end)
    end
end

function on_update(dt)
    -- Update all droppers
    for name, dropper in pairs(tycoonData.droppers) do
        dropper.timer = dropper.timer + dt
        if dropper.timer >= dropper.rate then
            dropper.timer = 0
            spawnFromDropper(dropper)
        end
    end
end

function spawnFromDropper(dropper)
    local part = Instance.new("Part")
    part.Name = "DroppedPart"
    part.Size = Vector3.new(1, 1, 1)
    part.Position = dropper.part.Position
    part.Color = Color3.fromRGB(255, 215, 0)
    
    local value = Instance.new("IntValue")
    value.Name = "Value"
    value.Value = dropper.value
    value.Parent = part
    
    part.Parent = workspace
end

function collectPart(hit)
    if hit.Name == "DroppedPart" then
        local value = hit:FindFirstChild("Value")
        if value then
            tycoonData.money = tycoonData.money + value.Value
            print("Money: $" .. tycoonData.money)
            hit:Destroy()
        end
    end
end
```

---

# 11. CHARACTER RIGGING

## Rig Structure

A basic character rig consists of:

```
Model (Character)
├── HumanoidRootPart (invisible center)
├── Torso
├── Head
├── Left Arm
├── Right Arm
├── Left Leg
├── Right Leg
├── Humanoid
└── Motor6D joints (connect parts)
```

## Creating a Rig via Script

```lua
function on_start()
    createRig("TestCharacter", Vector3.new(0, 10, 0))
end

function createRig(name, position)
    -- Create model container
    local char = Instance.new("Model")
    char.Name = name
    
    -- Create HumanoidRootPart (center)
    local hrp = Instance.new("Part")
    hrp.Name = "HumanoidRootPart"
    hrp.Size = Vector3.new(2, 2, 1)
    hrp.Position = position
    hrp.Transparency = 1  -- Invisible
    hrp.CanCollide = false
    hrp.Parent = char
    
    -- Create Torso
    local torso = Instance.new("Part")
    torso.Name = "Torso"
    torso.Size = Vector3.new(2, 2, 1)
    torso.Position = position
    torso.Color = Color3.fromRGB(163, 162, 165)
    torso.Parent = char
    
    -- Create Head
    local head = Instance.new("Part")
    head.Name = "Head"
    head.Size = Vector3.new(1, 1, 1)
    head.Position = position + Vector3.new(0, 1.5, 0)
    head.Color = Color3.fromRGB(245, 205, 175)
    head.Parent = char
    
    -- Create limbs
    createLimb(char, "Left Arm", position + Vector3.new(-1.5, 0, 0), Vector3.new(1, 2, 1))
    createLimb(char, "Right Arm", position + Vector3.new(1.5, 0, 0), Vector3.new(1, 2, 1))
    createLimb(char, "Left Leg", position + Vector3.new(-0.5, -2, 0), Vector3.new(1, 2, 1))
    createLimb(char, "Right Leg", position + Vector3.new(0.5, -2, 0), Vector3.new(1, 2, 1))
    
    -- Add Humanoid
    local humanoid = Instance.new("Humanoid")
    humanoid.MaxHealth = 100
    humanoid.Health = 100
    humanoid.Parent = char
    
    -- Connect parts with Motor6D
    connectParts(torso, head, "Neck")
    connectParts(torso, char:FindFirstChild("Left Arm"), "Left Shoulder")
    connectParts(torso, char:FindFirstChild("Right Arm"), "Right Shoulder")
    connectParts(torso, char:FindFirstChild("Left Leg"), "Left Hip")
    connectParts(torso, char:FindFirstChild("Right Leg"), "Right Hip")
    connectParts(hrp, torso, "Root")
    
    char.Parent = workspace
    print("Created rig: " .. name)
end

function createLimb(parent, name, position, size)
    local limb = Instance.new("Part")
    limb.Name = name
    limb.Size = size
    limb.Position = position
    limb.Color = Color3.fromRGB(245, 205, 175)
    limb.Parent = parent
    return limb
end

function connectParts(part0, part1, name)
    local motor = Instance.new("Motor6D")
    motor.Name = name
    motor.Part0 = part0
    motor.Part1 = part1
    motor.Parent = part0
    return motor
end
```

## Quick Rig Creation

Use the built-in function:

```lua
function on_start()
    -- Select multiple parts in studio
    -- Then group them
    -- Right-click → Group as Model + Humanoid (Rig)
    
    -- Or do it via script (in studio):
    -- Select parts, then run this
    local selectedParts = game:GetService("Selection"):Get()
    groupAsRig(selectedParts, "MyCharacter")
end
```

---

# 12. API REFERENCE

## Global Functions

```lua
print(...)                  -- Output to console
warn(...)                   -- Output warning
wait(seconds)               -- Pause execution
delay(time, func)           -- Call func after delay
spawn(func)                 -- Run func in new thread
tick()                      -- Current time in seconds
```

## Instance Methods

```lua
instance:Destroy()          -- Delete instance
instance:Clone()            -- Copy instance
instance:FindFirstChild(name) -- Find child by name
instance:GetChildren()      -- Array of all children
instance:IsA(className)     -- Check type
```

## Finding Objects

```lua
workspace:FindFirstChild("PartName")
script.Parent:FindFirstChild("Humanoid")
game:GetService("Players"):GetPlayers()
```

## Common Services

```lua
workspace                   -- Game world
game:GetService("Players")  -- Player management
game:GetService("Lighting") -- Lighting settings
```

## Useful Patterns

### Debounce (Prevent Spam)

```lua
local debounce = false

function on_start()
    part.Touched:Connect(onTouched)
end

function onTouched(hit)
    if debounce then return end
    debounce = true
    
    print("Touched!")
    -- Do action
    
    wait(1)  -- Cooldown
    debounce = false
end
```

### Looping Timer

```lua
local timer = 0
local interval = 5

function on_update(dt)
    timer = timer + dt
    
    if timer >= interval then
        timer = timer - interval  -- Keep remainder
        doAction()
    end
end

function doAction()
    print("Action every 5 seconds!")
end
```

### Distance Check

```lua
function on_update(dt)
    local target = workspace:FindFirstChild("Target")
    if target then
        local distance = (script.Parent.Position - target.Position).Magnitude
        
        if distance < 10 then
            print("Within 10 studs!")
        end
    end
end
```

---

# CHANGELOG v1.1

## New Features
- ✅ Multi-selection support (Ctrl+Click, Shift+Click)
- ✅ Group as Model / Group as Rig
- ✅ Advanced Properties panel (50+ properties)
- ✅ Color picker integration
- ✅ MEPIDE script editor tab
- ✅ Double-click Script to open
- ✅ Transform gizmos (Move/Rotate/Scale)
- ✅ Model position/rotation/scale properties

## Improvements
- Better synchronization between viewport and workspace tree
- Fixed color picker updating objects
- Removed duplicate MEPIDE panel
- Script objects now properly open in editor

## Bug Fixes
- Fixed gizmo crash on non-BasePart objects
- Fixed tree refresh with None objects
- Updated color picker to directly update obj.color
- Fixed script double-click handling

---

# QUICK REFERENCE CARD

## Essential Callbacks
```lua
function on_start()    -- Called once at Play
function on_update(dt) -- Called every frame
```

## Common Properties
```lua
part.Position = Vector3.new(x, y, z)
part.Rotation = Vector3.new(rx, ry, rz)
part.Size = Vector3.new(sx, sy, sz)
part.Color = Color3.fromRGB(r, g, b)
part.Transparency = 0.5
part.Anchored = true
```

## Events
```lua
part.Touched:Connect(function(hit) end)
humanoid.Died:Connect(function() end)
```

## Math
```lua
Vector3.new(x, y, z)
Color3.fromRGB(r, g, b)
math.random(min, max)
math.floor/ceil/round
```

## Instance
```lua
Instance.new("Part")
obj:Destroy()
obj:FindFirstChild("Name")
obj:GetChildren()
```

---

**© 2025 Micah Engine Studio**  
**Version 1.1.0 - Complete Reference**

For support, examples, and community projects, join the Discord!

Happy coding! 🎮✨
