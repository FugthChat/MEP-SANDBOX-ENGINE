# MEPLua Bible v1.3
## Complete Reference Manual for Micah Engine Studio

---

**Version:** 1.3.0  
**Engine:** Micah Engine Studio  
**Date:** December 2025  
**Author:** Fugth Chat LLC  

---

# 📖 TABLE OF CONTENTS

1. [Introduction](#1-introduction)
2. [Engine Overview](#2-engine-overview)
3. [Installation & Setup](#3-installation--setup)
4. [MEPLua Scripting Basics](#4-meplua-scripting-basics)
5. [Instance System](#5-instance-system)
6. [Data Types Reference](#6-data-types-reference)
7. [Properties Reference](#7-properties-reference)
8. [Events System](#8-events-system)
9. [API Reference](#9-api-reference)
10. [Example Projects](#10-example-projects)
11. [Troubleshooting](#11-troubleshooting)
12. [Changelog](#12-changelog)

---

# 1. INTRODUCTION

## What is Micah Engine Studio?

Micah Engine Studio (MEP) is a professional, standalone 3D game development engine for Windows. Designed for creators who want a lightweight, portable solution without heavy installations or dependencies.

### Key Features

- **Portable**: No installation required - extract and run
- **MEPLua Scripting**: Full Lua 5.4 runtime with custom API
- **50+ Object Types**: Parts, Models, Humanoids, Physics, and more
- **OpenGL Rendering**: Modern 3D graphics with depth testing
- **OBJ Import**: Load external 3D models
- **Project System**: Save/load .mep project files

### System Requirements

- **OS:** Windows 10/11 (64-bit)
- **RAM:** 4GB minimum, 8GB recommended
- **GPU:** OpenGL 3.3 compatible
- **Storage:** 500MB free space

---

# 2. ENGINE OVERVIEW

## Interface Layout

```
┌─────────────────────────────────────────────────────────┐
│  File   Edit   View   Insert   Run   Help               │
├─────────────┬─────────────────────────┬─────────────────┤
│  EXPLORER   │      3D VIEWPORT        │   PROPERTIES    │
│             │                         │                 │
│  Workspace  │     [Your Scene]        │   Name: Part    │
│   ├─ Part1  │                         │   Position: X,Y │
│   ├─ Model  │                         │   Size: 4,1,2   │
│   │  └─ ..  │                         │   Color: ■      │
│   └─ Script │                         │   Anchored: ☑   │
│             │                         │                 │
├─────────────┴─────────────────────────┴─────────────────┤
│  OUTPUT                                                  │
│  > Hello from MEPLua!                                   │
│  > Game started                                         │
└─────────────────────────────────────────────────────────┘
```

## Core Components

| Component | Description |
|-----------|-------------|
| **Explorer** | Hierarchical view of all objects in your project |
| **3D Viewport** | Interactive scene view with camera controls |
| **Properties** | Edit selected object's properties |
| **Output** | Console for print() and debug messages |
| **Script Editor** | Code editor for MEPLua scripts |

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+S` | Save project |
| `Ctrl+O` | Open project |
| `Ctrl+N` | New project |
| `F5` | Play/Stop |
| `Delete` | Delete selected |
| `Ctrl+D` | Duplicate |
| `Ctrl+Z` | Undo |
| `W/A/S/D` | Camera movement |
| `Right Mouse` | Camera rotation |

---

# 3. INSTALLATION & SETUP

## Quick Start

1. **Download** `MicahEngineStudio_v1.3.rar` from GitHub releases
2. **Extract** to any folder (Desktop, Documents, USB drive)
3. **Run** `MicahEngineStudio.exe`
4. **Create** a new project or open an existing one

## Folder Structure

```
MicahEngineStudio_v1.3/
├── MicahEngineStudio.exe    # Main application
├── assets/                   # Engine assets
│   ├── textures/
│   ├── shaders/
│   └── fonts/
├── projects/                 # Your saved projects
└── docs/                     # Documentation
```

## First Project

1. Launch the engine
2. Click **File > New Project**
3. Name your project
4. Right-click **Workspace** in Explorer
5. Select **Insert Object > Parts > Part**
6. Press **F5** to play!

---

# 4. MEPLUA SCRIPTING BASICS

## What is MEPLua?

MEPLua is the scripting language for Micah Engine Studio. It's based on Lua 5.4 with custom APIs for 3D game development.

## Creating Your First Script

1. Right-click a Part in Explorer
2. Select **Insert Object > Scripting > Script**
3. Double-click the Script to open the editor
4. Write your code:

```lua
-- My first MEPLua script!
function on_start()
    print("Hello, Micah Engine!")
    
    -- Access the part this script is attached to
    local myPart = script.Parent
    myPart.Color = Color3.fromRGB(255, 0, 0)  -- Make it red
    
    print("Part name: " .. myPart.Name)
end
```

5. Press **F5** to run

## Script Lifecycle

### on_start()

Called **once** when you press Play:

```lua
function on_start()
    print("Game initialized!")
    
    -- Setup code here
    local part = script.Parent
    part.Anchored = true
end
```

### on_update(dt)

Called **every frame** (60 times per second). `dt` = delta time:

```lua
local angle = 0

function on_update(dt)
    -- Rotate 90 degrees per second
    angle = angle + (90 * dt)
    script.Parent.Rotation = Vector3.new(0, angle, 0)
end
```

## Variables & Types

```lua
-- Numbers
local health = 100
local speed = 16.5

-- Strings
local playerName = "Player1"

-- Booleans
local isAlive = true
local canJump = false

-- Tables (arrays/dictionaries)
local inventory = {"Sword", "Shield", "Potion"}
local stats = {health = 100, mana = 50}
```

## Control Flow

```lua
-- If statements
if health <= 0 then
    print("Game Over!")
elseif health < 20 then
    print("Low health!")
else
    print("Healthy")
end

-- For loops
for i = 1, 10 do
    print("Count: " .. i)
end

-- While loops
while isAlive do
    -- Game loop
    wait(1)
end
```

---

# 5. INSTANCE SYSTEM

## Creating Objects at Runtime

Use `Instance.new()` to create objects dynamically:

```lua
function on_start()
    -- Create a new Part
    local newPart = Instance.new("Part")
    newPart.Name = "SpawnedPart"
    newPart.Position = Vector3.new(0, 10, 0)
    newPart.Size = Vector3.new(2, 2, 2)
    newPart.Color = Color3.fromRGB(0, 255, 0)
    newPart.Parent = workspace  -- Add to scene
end
```

## Available Instance Types

### Parts & Shapes
| Class | Description |
|-------|-------------|
| `Part` | Standard cube/box |
| `Sphere` | Spherical object |
| `Cylinder` | Cylindrical object |
| `WedgePart` | Wedge/ramp shape |
| `CornerWedgePart` | Corner wedge |
| `MeshPart` | Custom imported mesh |

### Gameplay
| Class | Description |
|-------|-------------|
| `Model` | Container for parts |
| `Humanoid` | Character controller |
| `Tool` | Equippable item |
| `SpawnLocation` | Player spawn point |

### Scripting
| Class | Description |
|-------|-------------|
| `Script` | Server-side script |
| `LocalScript` | Client-side script |
| `ModuleScript` | Reusable code module |
| `BindableEvent` | Custom event |
| `BindableFunction` | Custom function |

### Physics
| Class | Description |
|-------|-------------|
| `BodyVelocity` | Apply velocity force |
| `BodyPosition` | Move to target position |
| `BodyGyro` | Control rotation |
| `Explosion` | Create explosion effect |

### Rigging
| Class | Description |
|-------|-------------|
| `Motor6D` | Animated joint |
| `Weld` | Fixed joint |
| `Attachment` | Connection point |

### Values
| Class | Description |
|-------|-------------|
| `BoolValue` | Store boolean |
| `IntValue` | Store integer |
| `NumberValue` | Store number |
| `StringValue` | Store string |
| `Vector3Value` | Store Vector3 |
| `ObjectValue` | Store object reference |
| `Color3Value` | Store color |

### Audio & Visual
| Class | Description |
|-------|-------------|
| `Sound` | Audio playback |
| `Decal` | Surface image |
| `Texture` | Repeating texture |
| `Camera` | View camera |
| `Light` | Point/Spot light |

## Finding Objects

```lua
-- Find child by name
local part = workspace:FindFirstChild("MyPart")

-- Get all children
local children = workspace:GetChildren()
for _, child in ipairs(children) do
    print(child.Name)
end

-- Check object type
if part:IsA("Part") then
    print("It's a Part!")
end
```

## Destroying Objects

```lua
local part = script.Parent
wait(5)  -- Wait 5 seconds
part:Destroy()  -- Remove from game
```

---

# 6. DATA TYPES REFERENCE

## Vector3

3D position, direction, or size:

```lua
-- Creation
local pos = Vector3.new(10, 5, -3)

-- Access components
print(pos.X, pos.Y, pos.Z)  -- 10, 5, -3

-- Math operations
local v1 = Vector3.new(1, 0, 0)
local v2 = Vector3.new(0, 1, 0)
local sum = v1 + v2         -- (1, 1, 0)
local diff = v1 - v2        -- (1, -1, 0)
local scaled = v1 * 5       -- (5, 0, 0)

-- Properties
print(pos.Magnitude)        -- Length (~11.6)
print(pos.Unit)             -- Normalized direction

-- Common directions
local UP = Vector3.new(0, 1, 0)
local FORWARD = Vector3.new(0, 0, -1)
local RIGHT = Vector3.new(1, 0, 0)
```

## Color3

RGB color values:

```lua
-- From 0-1 range
local red = Color3.new(1, 0, 0)
local white = Color3.new(1, 1, 1)

-- From 0-255 range (recommended)
local blue = Color3.fromRGB(0, 0, 255)
local purple = Color3.fromRGB(128, 0, 255)
local teal = Color3.fromRGB(0, 200, 200)

-- From HSV (Hue, Saturation, Value)
local rainbow = Color3.fromHSV(0.5, 1, 1)

-- Access components
print(red.R, red.G, red.B)  -- 1, 0, 0
```

## CFrame

Position + Rotation (Coordinate Frame):

```lua
-- Create at position
local cf = CFrame.new(10, 5, 0)

-- Create with rotation (radians)
local rotated = CFrame.Angles(0, math.rad(45), 0)

-- Combine position and rotation
local combined = CFrame.new(10, 5, 0) * CFrame.Angles(0, math.rad(45), 0)

-- Apply to part
part.CFrame = cf
```

---

# 7. PROPERTIES REFERENCE

## BasePart Properties

All parts share these properties:

### Transform
```lua
part.Position = Vector3.new(x, y, z)     -- World position
part.Rotation = Vector3.new(rx, ry, rz)  -- Euler angles (degrees)
part.Size = Vector3.new(sx, sy, sz)      -- Dimensions
part.Scale = Vector3.new(1, 1, 1)        -- Scale multiplier
part.CFrame = CFrame.new(x, y, z)        -- Position + Rotation
```

### Appearance
```lua
part.Color = Color3.fromRGB(r, g, b)     -- RGB color
part.Transparency = 0.5                   -- 0=opaque, 1=invisible
part.Reflectance = 0.3                    -- 0-1 shininess
part.Material = "Plastic"                 -- Material type
```

### Physics
```lua
part.Anchored = true                      -- Fixed in place
part.CanCollide = true                    -- Solid collision
part.Velocity = Vector3.new(vx, vy, vz)  -- Current velocity
part.Mass = 10.0                          -- Mass value
```

### Identity
```lua
part.Name = "MyPart"                      -- Object name
part.Locked = false                       -- Locked in editor
part.Visible = true                       -- Visibility
```

## Humanoid Properties

```lua
humanoid.Health = 100                     -- Current HP
humanoid.MaxHealth = 100                  -- Maximum HP
humanoid.WalkSpeed = 16                   -- Movement speed
humanoid.JumpPower = 50                   -- Jump strength
humanoid.AutoRotate = true                -- Face movement direction
humanoid.PlatformStand = false            -- Ragdoll state
```

## Model Properties

```lua
model.Name = "MyModel"                    -- Model name
model.PrimaryPart = model.Head            -- Main reference part
model.Position = Vector3.new(0, 5, 0)     -- Move entire model
model.Rotation = Vector3.new(0, 45, 0)    -- Rotate entire model
```

---

# 8. EVENTS SYSTEM

## Connecting to Events

```lua
function on_start()
    local part = script.Parent
    
    -- Connect event to function
    part.Touched:Connect(function(otherPart)
        print("Touched by: " .. otherPart.Name)
    end)
end
```

## Part Events

### Touched
Fires when another part touches:

```lua
part.Touched:Connect(function(hit)
    local humanoid = hit.Parent:FindFirstChild("Humanoid")
    if humanoid then
        print("Player touched!")
    end
end)
```

### TouchEnded
Fires when contact ends:

```lua
part.TouchEnded:Connect(function(hit)
    print("No longer touching: " .. hit.Name)
end)
```

## Humanoid Events

### Died
Fires when health reaches 0:

```lua
humanoid.Died:Connect(function()
    print("Character died!")
end)
```

### HealthChanged
Fires when health changes:

```lua
humanoid.HealthChanged:Connect(function(newHealth)
    print("Health: " .. newHealth)
end)
```

---

# 9. API REFERENCE

## Global Functions

| Function | Description |
|----------|-------------|
| `print(...)` | Output to console |
| `warn(...)` | Output warning (yellow) |
| `wait(seconds)` | Pause execution |
| `delay(time, func)` | Call function after delay |
| `spawn(func)` | Run function in new thread |
| `tick()` | Current time in seconds |

## Instance Methods

| Method | Description |
|--------|-------------|
| `Instance.new(className)` | Create new instance |
| `obj:Destroy()` | Delete instance |
| `obj:Clone()` | Copy instance |
| `obj:FindFirstChild(name)` | Find child by name |
| `obj:GetChildren()` | Get all children |
| `obj:IsA(className)` | Check class type |

## Math Library

| Function | Description |
|----------|-------------|
| `math.random()` | Random 0-1 |
| `math.random(n)` | Random 1-n |
| `math.random(a, b)` | Random a-b |
| `math.floor(x)` | Round down |
| `math.ceil(x)` | Round up |
| `math.abs(x)` | Absolute value |
| `math.sqrt(x)` | Square root |
| `math.sin/cos/tan(x)` | Trigonometry |
| `math.rad(deg)` | Degrees to radians |
| `math.deg(rad)` | Radians to degrees |

---

# 10. EXAMPLE PROJECTS

## Kill Brick

```lua
-- Classic instant-death obstacle
local killBrick = script.Parent

function on_start()
    killBrick.Touched:Connect(function(hit)
        local humanoid = hit.Parent:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.Health = 0
        end
    end)
end
```

## Spinning Part

```lua
local rotation = 0

function on_update(dt)
    rotation = rotation + (90 * dt)
    script.Parent.Rotation = Vector3.new(0, rotation, 0)
end
```

## Color Changer

```lua
local colors = {
    Color3.fromRGB(255, 0, 0),
    Color3.fromRGB(0, 255, 0),
    Color3.fromRGB(0, 0, 255),
}
local index = 1

function on_start()
    script.Parent.Touched:Connect(function()
        index = index + 1
        if index > #colors then index = 1 end
        script.Parent.Color = colors[index]
    end)
end
```

## Projectile Spawner

```lua
function on_start()
    while true do
        spawnProjectile()
        wait(2)
    end
end

function spawnProjectile()
    local bullet = Instance.new("Sphere")
    bullet.Name = "Bullet"
    bullet.Size = Vector3.new(1, 1, 1)
    bullet.Color = Color3.fromRGB(255, 255, 0)
    bullet.Position = script.Parent.Position
    bullet.Parent = workspace
    
    local velocity = Instance.new("BodyVelocity")
    velocity.Velocity = Vector3.new(0, 0, -50)
    velocity.Parent = bullet
    
    delay(5, function()
        bullet:Destroy()
    end)
end
```

---

# 11. TROUBLESHOOTING

## Common Issues

### Script Not Running
- Check script is under a Part or Model
- Make sure `on_start()` is defined
- Check Output panel for errors

### Object Not Visible
- Check `Transparency` is not 1
- Check `Visible` is true
- Check Position is in view

### Physics Not Working
- Set `Anchored = false`
- Set `CanCollide = true`
- Add physics forces

### Performance Issues
- Avoid creating objects in `on_update()`
- Use object pooling
- Limit print() calls

---

# 12. CHANGELOG

## v1.3 (December 2025)
- ✅ New launcher with branding removal
- ✅ Stability improvements
- ✅ Crash recovery
- ✅ Memory optimizations
- ✅ Error logging system

## v1.2
- ✅ Instance.new() system
- ✅ Event connections
- ✅ Motor6D rigging
- ✅ OBJ import

## v1.1
- ✅ MEPLua runtime
- ✅ Vector3/Color3/CFrame
- ✅ Property editor
- ✅ Project save/load

## v1.0
- ✅ Initial release
- ✅ OpenGL renderer
- ✅ Basic scripting
- ✅ 3D viewport

---

# 📥 DOWNLOADS

**Engine:** [MicahEngineStudio_v1.3.rar](https://github.com/FugthChat/MEP-SANDBOX-ENGINE/releases/download/v1.3/MicahEngineStudio_v1.3.rar)

**Documentation:** [MEPLUABIBLE.pdf](https://github.com/FugthChat/MEP-SANDBOX-ENGINE/releases/download/v1.3/MEPLUABIBLE.pdf)

**Discord:** [discord.gg/BsUQUFYBmN](https://discord.gg/BsUQUFYBmN)

**GitHub:** [github.com/FugthChat/MEP-SANDBOX-ENGINE](https://github.com/FugthChat/MEP-SANDBOX-ENGINE)

---

**© 2025 Fugth Chat LLC. All rights reserved.**

*MEPLua Bible v1.3 - Complete Reference Manual*
