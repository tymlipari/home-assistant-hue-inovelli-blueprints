# 🏡 Home Assistant Inovelli Hue Blueprints

This repository contains reusable, dynamic blueprints for combining **Inovelli paddle dimmers** (via ZHA) with **Philips Hue lights and scenes** — featuring adaptive dimming, button-based scene cycling, and default scene recall.

These automations are purpose-built for flexible, state-aware lighting control that updates as your Hue rooms and scenes evolve.

---

## ✨ Features

### 💡 Unified Paddle Dimming
- Paddle **hold** = dim up or down smoothly
- Paddle **release** = stop dimming immediately
- Dynamic dimming via `input_boolean.dimmer_<room>`

### 🎬 Scene Cycling (Button 3)
- Button **3 press** = cycle forward through Hue scenes
- Button **3 hold** = cycle backward
- Scenes discovered dynamically for each Hue room
- State tracked using `input_number.scene_index_<room>`

### 🌟 Default Scene Activation
- Optionally activate a scene when `light.<room>` turns on
- Works whether light is triggered by switch, app, or automation

### 🧠 Clean Entity Naming Convention
- `light.<room>` for Hue Room or Zone
- `input_boolean.dimmer_<room>` for dimming control
- `input_number.scene_index_<room>` for scene tracking

---

## 🛠 Requirements

For each room (e.g. `OfficeFan`), create the following:

| Entity | Example | Purpose |
|--------|---------|---------|
| Hue Light Group | `light.officefan` | Hue Room (sync target) |
| `input_boolean` | `input_boolean.dimmer_officefan` | Controls loop for dimming script |
| `input_number` | `input_number.scene_index_officefan` | Tracks active scene index |
| Hue Scenes | `scene.officefan_relax`, etc. | Must follow naming pattern: `scene.<room>_<name>` |

---

## 📁 Included Blueprints

### 🧠 `Hue Paddle Dimming + Scene Cycling (ZHA Event)`
Path: `blueprints/automation/inovelli/hue_dimmer_zha_unified.yaml`

Handles:
- Dimming start/stop via paddle
- Scene cycling (forward/back)
- Default scene activation
- Detailed logging for troubleshooting

### 🔧 `Hue Room Dimmer - Dynamic Up/Down`
Path: `blueprints/script/inovelli/dim_hue_room_lights.yaml`

Handles:
- Smooth dimming loop
- Customizable brightness step
- Parameterized by `room`, `direction`, and `step`

---

## 🧪 Example Use Case

1. Create a room in the Hue app named `OfficeFan`
2. Add matching helpers:
   - `input_boolean.dimmer_officefan`
   - `input_number.scene_index_officefan`
3. Add or sync scenes like `scene.officefan_relax`, `scene.officefan_energize`
4. Create a script from the dimmer blueprint with room = `OfficeFan`
5. Create an automation from the unified automation blueprint and link it to the script

Now your Inovelli switch will:
- Dim the Hue room precisely on hold
- Stop on release
- Cycle through available scenes using button 3
- Activate a default scene (if configured)

---

## 🔍 Resources

- [Blueprint Exchange Thread (coming soon)](https://community.home-assistant.io/c/blueprints-exchange/)
- [Inovelli Blue Devices + ZHA](https://community.inovelli.com/)
- [Philips Hue Integration](https://www.home-assistant.io/integrations/hue/)
- Created by [@Ratoka](https://github.com/Ratoka)

---

## 🧾 License

MIT License — see `LICENSE` file
