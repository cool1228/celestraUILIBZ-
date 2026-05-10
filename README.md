[README.md](https://github.com/user-attachments/files/27566845/README.md)
# Celestra UI Library

A clean, dark-themed Roblox UI library with smooth animations, a full element set, and a built-in SaveManager for config persistence.

> **Made entirely by [Claude](https://claude.ai) (Anthropic) — AI-generated Roblox UI library.**

---

## Preview

```
┌─────────────────────────────────────────────────────────────┐
│  Celestra  [BETA] [PAID] [v0.1.0]               −  ×        │
├──────────┬──────────────────────────────────────────────────┤
│  MAIN    │  ┌─ TOGGLES ──────────────────────────────────┐  │
│  › Test  │  │  ESP                              [ ]      │  │
│          │  │  Aimbot                           [■]      │  │
│ SETTINGS │  └────────────────────────────────────────────┘  │
│  › Config│  ┌─ SLIDERS ──────────────────────────────────┐  │
│          │  │  FOV Circle              ██████░░░  120     │  │
│          │  └────────────────────────────────────────────┘  │
├──────────┴──────────────────────────────────────────────────┤
│  ● Status: Connected          ● Game: Example               │
└─────────────────────────────────────────────────────────────┘
```

---

## Load

```lua
local Celestra = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/cool1228/celestraUILIBZ-/refs/heads/main/libary.txt"
))()
```

---

## Quick Start

```lua
local Celestra = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/cool1228/celestraUILIBZ-/refs/heads/main/libary.txt"
))()

local Window = Celestra:CreateWindow({
    Title       = "Celestra",
    Width       = 850,
    Height      = 540,
    ToggleKey   = Enum.KeyCode.RightShift,
    Status      = "Status: Ready",
    StatusRight = "Game: Test",
    Badges      = {
        { text = "BETA",   type = "accent"  },
        { text = "PAID",   type = "danger"  },
        { text = "v0.1.0", type = "default" },
    },
})

local cat  = Window:AddCategory("Main")
local page = cat:AddPage("Home")
local card = page:AddCard("Settings")

card:AddToggle("myToggle", {
    Title    = "Enable Feature",
    Desc     = "Turns the feature on or off.",
    Default  = false,
    Callback = function(value) print(value) end,
})
```

---

## CreateWindow Options

| Option | Type | Default | Description |
|---|---|---|---|
| `Title` | string | `"Celestra"` | Window title shown in the top-left |
| `Width` | number | `850` | Window width in pixels |
| `Height` | number | `540` | Window height in pixels |
| `ToggleKey` | KeyCode | `RightShift` | Key to show/hide the window |
| `Status` | string | `"Status: Ready"` | Left status bar text |
| `StatusRight` | string | `""` | Right status bar text |
| `Badges` | table | `{}` | Array of badge objects (see below) |

### Badges

Badges appear in the title bar next to the window title. You can add as many as you want or remove them all.

```lua
Badges = {
    { text = "BETA",   type = "accent"  },  -- blue
    { text = "PAID",   type = "danger"  },  -- red
    { text = "v0.1.0", type = "default" },  -- grey
}
```

| Type | Color | Use for |
|---|---|---|
| `"accent"` | Blue | Feature tags: BETA, NEW, PRO |
| `"danger"` | Red | Warning tags: PAID, ADMIN, DEV |
| `"default"` | Grey | Info tags: version numbers, build IDs |

---

## Structure

```
Window
 └── Category  (sidebar group header)
      └── Page  (sidebar nav item)
           └── Card  (content section with a header)
                └── Elements (Toggle, Slider, Dropdown, ...)
```

```lua
local cat  = Window:AddCategory("Main")
local page = cat:AddPage("Home")
local card = page:AddCard("My Settings")
```

---

## Elements

### Toggle

```lua
local elem = card:AddToggle("uniqueId", {
    Title    = "My Toggle",
    Desc     = "Optional description.",
    Default  = false,
    Callback = function(value) print(value) end,
})

elem:GetValue()       -- returns true/false
elem:SetValue(true)   -- set programmatically
```

---

### Slider

```lua
local elem = card:AddSlider("uniqueId", {
    Title    = "My Slider",
    Desc     = "Optional description.",
    Min      = 0,
    Max      = 100,
    Default  = 50,
    Callback = function(value) print(value) end,
})

elem:GetValue()     -- returns current number
elem:SetValue(75)   -- set programmatically
```

---

### Dropdown

```lua
local elem = card:AddDropdown("uniqueId", {
    Title    = "My Dropdown",
    Desc     = "Optional description.",
    Options  = { "Option A", "Option B", "Option C" },
    Default  = "Option A",
    Callback = function(value) print(value) end,
})

elem:GetValue()                           -- returns selected string
elem:SetValue("Option B")                 -- change selected item
elem:SetOptions({ "New A", "New B" })     -- fully replace the option list
```

---

### Keybind

```lua
local elem = card:AddKeybind("uniqueId", {
    Title    = "My Keybind",
    Desc     = "Click the button, then press a key.",
    Default  = "E",
    Callback = function(key) print(key) end,
})

elem:GetValue()        -- returns key name string e.g. "E"
elem:SetValue("F")     -- set programmatically
```

---

### Color Picker

```lua
local elem = card:AddColorPicker("uniqueId", {
    Title    = "My Color",
    Desc     = "Click the swatch to open the picker.",
    Default  = Color3.fromRGB(255, 80, 80),
    Callback = function(color) print(color) end,
})

elem:GetValue()                          -- returns Color3
elem:SetValue(Color3.fromRGB(0,255,0))   -- set programmatically
```

---

### Text Input

```lua
local elem = card:AddTextInput("uniqueId", {
    Title       = "My Input",
    Desc        = "Optional description.",
    Placeholder = "Type here...",
    Default     = "",
    Callback    = function(value) print(value) end,
})

elem:GetValue()          -- returns string
elem:SetValue("hello")   -- set programmatically
```

---

### Button

```lua
card:AddButton("uniqueId", {
    Title      = "My Button",
    Desc       = "Optional description.",
    ButtonText = "Execute",
    Danger     = false,   -- set true for a red danger-style button
    Callback   = function() print("clicked") end,
})
```

---

### Label

```lua
local elem = card:AddLabel({
    Text     = "Some information text.",
    Color    = Color3.fromRGB(130, 130, 130),
    TextSize = 12,
})

elem:SetText("Updated text")
elem:SetColor(Color3.fromRGB(255, 100, 100))
```

---

### Divider

```lua
card:AddDivider()   -- draws a thin horizontal line between elements
```

---

## SaveManager

Handles saving, loading, and deleting named config files locally.

### Load

```lua
local SaveManager = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/cool1228/celestraUILIBZ-/refs/heads/main/addons/SaveManager"
))()
```

### Setup

```lua
SaveManager:SetWindow(Window)   -- must be called before BuildConfigPage

local settingsCat = Window:AddCategory("Settings")
local configPage  = settingsCat:AddPage("Config")
SaveManager:BuildConfigPage(configPage)

SaveManager:LoadAutoload()   -- auto-loads last saved config on startup
```

### Config page buttons

| Button | Action |
|---|---|
| **Save** | Saves current settings under the typed name |
| **Load** | Loads the selected config from the dropdown |
| **Overwrite** | Overwrites the selected config with current settings |
| **Delete** | Deletes the selected config file |
| **Set Autoload** | Marks the selected config to auto-load every run |
| **Reset Autoload** | Clears the autoload so nothing loads on startup |

### API

```lua
SaveManager:Save("myConfig")          -- save to file
SaveManager:Load("myConfig")          -- load from file
SaveManager:Delete("myConfig")        -- delete file
SaveManager:SetFolder("MyFolder")     -- change storage folder (default: CelestraSettings)
SaveManager:SetIgnoreIndexes({"id1"}) -- exclude elements from being saved
```

---

## Window API

```lua
Window:SetStatus("Status: Active", "Players: 12")   -- update status bar
Window:GetValue("elementId")                         -- get any element's value by ID
Window:GetElement("elementId")                       -- get element object by ID
Window:Destroy()                                     -- remove the UI entirely
```

---

## Full Example

See [`Example.lua`](Example.lua) in this repository for a complete working script that demonstrates every element type.

---

## Credits

| | |
|---|---|
| **UI Library** | Built entirely by [Claude](https://claude.ai) (Anthropic AI) |
| **SaveManager** | Built entirely by [Claude](https://claude.ai) (Anthropic AI) |
| **Repository** | [cool1228](https://github.com/cool1228) |

> Celestra was designed and coded from scratch by Claude (claude.ai), Anthropic's AI assistant, across an iterative development session covering layout, scrolling, input handling, animations, and the config system.

---

## License

Free to use and modify. Credit appreciated but not required.
