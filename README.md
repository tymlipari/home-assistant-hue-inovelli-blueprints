[![Import Blueprint: Automation](https://img.shields.io/badge/Home%20Assistant-Import%20Automation-blue?logo=home-assistant)](https://my.home-assistant.io/redirect/blueprint_import/?repository_url=https://github.com/Ratoka/homeassistant-inovelli-hue-blueprints&filepath=blueprints/automation/inovelli/hue_dimmer_zha_unified.yaml)

[![Import Blueprint: Script](https://img.shields.io/badge/Home%20Assistant-Import%20Script-blue?logo=home-assistant)](https://my.home-assistant.io/redirect/blueprint_import/?repository_url=https://github.com/Ratoka/homeassistant-inovelli-hue-blueprints&filepath=blueprints/script/inovelli/dim_hue_room_lights.yaml)

# 🏡 Home Assistant Inovelli Hue Blueprints

Reusable, dynamic blueprints for combining **Inovelli paddle dimmers** (via ZHA) with **Philips Hue lights and scenes**. Features include adaptive dimming, button-based scene cycling, default scene recall, and robust state tracking.

---

## ✨ Features

### 💡 Paddle Dimming (Hold/Release)
- **Hold up/down**: Smoothly dims Hue room lights up or down
- **Release**: Instantly stops dimming
- Dimming is managed via a dedicated script and `input_boolean.dimmer_<room>`

### 🎬 Scene Cycling (Button 3)
- **Button 3 press**: Cycles forward through all Hue scenes for the room
- **Button 3 hold**: Cycles backward through scenes
- Scenes are discovered dynamically (no hardcoding)
- Scene index tracked with `input_number.scene_index_<room>`

### 🌟 Default Scene Activation
- Optionally activate a default scene when `light.<room>` turns on
- Works with switch, app, or automation triggers

### 🧠 Entity Naming Convention
- `light.<room>`: Hue Room or Zone group
- `input_boolean.dimmer_<room>`: Dimming control helper
- `input_number.scene_index_<room>`: Scene index tracker
- `scene.<room>_<name>`: Hue scenes (must follow this pattern)

### 📝 Logging & Troubleshooting
- Detailed logbook entries for all actions and state changes

---

## 🛠 Requirements

For each room (e.g. `Office`), create the following:

| Entity | Example | Purpose |
|--------|---------|---------|
| Hue Light Group | `light.office` | Hue Room (sync target) |
| `input_boolean` | `input_boolean.dimmer_office` | Controls dimming script loop |
| `input_number` | `input_number.scene_index_office` | Tracks active scene index |
| Hue Scenes | `scene.office_relax`, `scene.office_energize`, etc. | Must follow `scene.<room>_<name>` |

---

## 📁 Included Blueprints

### 🧠 `Hue Paddle Dimming + Scene Cycling (ZHA Event)`
Path: `blueprints/automation/inovelli/hue_dimmer_zha_unified.yaml`

Handles:
- Paddle dimming (hold/release)
- Scene cycling (forward/back)
- Default scene activation
- Logging for troubleshooting

### 🔧 `Hue Room Dimmer - Dynamic Up/Down`
Path: `blueprints/script/inovelli/dim_hue_room_lights.yaml`

Handles:
- Smooth dimming loop for a Hue room
- Customizable brightness step and direction
- Parameterized by `room`, `direction`, and `step`

---

## 🧪 Example Use Case

1. Create a room in the Hue app named `Office`
2. Add matching helpers in Home Assistant:
   - `input_boolean.dimmer_office`
   - `input_number.scene_index_office`
3. Add or sync scenes like `scene.office_relax`, `scene.office_energize`
4. Create a script from the dimmer blueprint with `room = Office`
5. Create an automation from the unified automation blueprint and link it to the script

Now your Inovelli switch will:
- Dim the Hue room lights smoothly on paddle hold
- Stop dimming on release
- Cycle through available scenes using button 3
- Optionally activate a default scene when the room is turned on

---

## 🔍 Resources

- [Blueprint Exchange Thread (coming soon)](https://community.home-assistant.io/c/blueprints-exchange/)
- [Inovelli Blue Devices + ZHA](https://community.inovelli.com/)
- [Philips Hue Integration](https://www.home-assistant.io/integrations/hue/)
- Created by [@Ratoka](https://github.com/Ratoka)

---

## 🧾 License

MIT License — see `LICENSE` file