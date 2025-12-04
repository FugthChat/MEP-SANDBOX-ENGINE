# 🎮 Micah Engine Studio v1.1

**Professional Roblox-inspired world builder with scripted gameplay tools.**

Version **1.1** delivers production-ready features: multi-selection, model grouping, rigging tools, advanced properties, color picker, and full MEPLua script integration.

---

## 🚀 Quick Start

```bash
python MICAHESANDBOXLAUNCHER.py
```

The launcher boots the virtual environment, installs dependencies, validates OpenGL, and starts the studio. No manual setup needed.

---

## ✨ Feature Highlights

### 🏢 Roblox-Style Layout
- Central **viewport/script tab stack** (viewport + unlimited script tabs)
- Left docks: **Toolbox** (transform modes, snapping, prefab list) + **World Settings** (grid, lighting, sky color)
- Right docks: **Explorer** hierarchy + **Properties Inspector** with visibility/lock toggles, script list, color picker
- Bottom tabs: Console, MEPLUA IDE, Output, Diagnostics

### 🎯 Smart Transform Gizmos
- Select / Move / Scale / Rotate modes with highlighted RGB gizmos
- Snapping for translation, rotation, scale (0.25 studs, 15° etc.)
- Precision syncing: property panel updates live while dragging
- Frame selection (F) and middle-mouse panning for quick navigation

### 📚 Workspace & Prefabs
- Roblox-like Explorer tree with visibility checkboxes and context menu (rename, duplicate, delete, lock)
- Prefab toolbox (Basic Part, Pillar, Mega Sphere, Ground Plane, Pyramid)
- Script attachments show under objects and in a dedicated “Scripts” root

### 🧱 Asset Pipeline
- OBJ importer with vertex/face parsing
- OBJ exporter for both primitives and custom meshes
- Scene save/load (`.json`) capturing camera settings and colors

### 🧠 Scripting Workflow
- Multi-tab MEPLUA/Lua editor (syntax highlighting, Ctrl+D duplicate, tab focus from Explorer)
- Bottom IDE panel with Run/Stop/New/Save/Load controls
- Attach scripts to objects, double-click to open

### 📊 Diagnostics & Quality-of-Life
- Built-in diagnostics log, console timestamps, scene stats
- Camera speed presets, world ambient slider, wireframe toggle
- Auto-updating status bar + dirty-state window title

---

## 📁 Project Structure

```
Micah-Engine-Studio/
├── MICAHESANDBOXLAUNCHER.py     # Universal launcher
├── README.md                    # This guide
├── requirements.txt             # Python deps
└── game_engine/
    ├── engine_studio.py         # Roblox-style editor (current)
    ├── engine_pro_gui.py        # Legacy backup
    └── engine/                  # Low-level systems
```

---

## 🕹️ Workflow Cheat Sheet

1. **Launch** `python MICAHESANDBOXLAUNCHER.py`
2. **Spawn prefabs** from Toolbox or add/import parts via Explorer
3. **Select** object in Explorer or viewport
4. **Transform** with gizmos (enable snapping if needed)
5. **Edit** numeric properties, color, visibility, lock state in Inspector
6. **Attach scripts** and open them in overlay tabs
7. **Save** project (`Ctrl+S`) or export models as OBJ

### Camera & Gizmos
| Action | Control |
| --- | --- |
| Move camera | `W A S D` |
| Raise / Lower | `E / Q` |
| Orbit | Right-click drag |
| Pan | Middle-click drag |
| Zoom | Mouse wheel |
| Frame selection | `F` or “Frame” button |

### Shortcuts
- `Ctrl+S` save project
- `Ctrl+D` duplicate selection
- `Delete` remove selection
- `F` focus camera

---

## 🗺️ What's New (v2.0)

- ✅ Full dock-based UI with toolbox, explorer, properties, world settings
- ✅ Prefab catalog + object context menu
- ✅ Snapping system for move/rotate/scale
- ✅ Rotate gizmo support & synchronized inspector updates
- ✅ Attached script list + script nodes in Explorer
- ✅ Grid, lighting, wireframe, ambient, sky-color controls
- ✅ Diagnostics tab and status logging
- ✅ OBJ export for custom + primitive meshes

Coming up next: Lua runtime binding, physics helpers, asset browser search, and visual scripting.

---

## Troubleshooting

| Issue | Fix |
| --- | --- |
| Gizmo won't grab | Ensure Move/Scale/Rotate mode active, hover directly over colored axis, check object not locked |
| Object invisible | Toggle checkbox next to object in Explorer or Inspector “Visible” toggle |
| Selection drifts | Disable snapping or reduce snap values in Toolbox |
| Import fails | OBJ must contain vertex/face lines; try re-exporting with triangulation |
| Camera lost | Press `F` with object selected or View → Reset Camera |

---

## Quick Reference Card

```
LAUNCH   : python MICAHESANDBOXLAUNCHER.py
SELECT   : Left-click in viewport or Explorer tree
GIZMOS   : Red=X, Green=Y, Blue=Z (rotate/scale supported)
SNAP     : Toolbox ▸ Enable + choose increments
SCRIPTS  : Attach in Inspector ▸ double-click to open
EXPORT   : File ▸ Save Project or Toolbox ▸ Export OBJ
```

---

**Made with ❤️ by Micah** · Active development ⚡

Enjoy building! 🎨✨
