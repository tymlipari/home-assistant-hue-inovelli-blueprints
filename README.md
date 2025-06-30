[![Import Blueprint: Automation](https://img.shields.io/badge/Home%20Assistant-Import%20Automation-blue?logo=home-assistant)](https://my.home-assistant.io/redirect/blueprint_import/?repository_url=https://github.com/Ratoka/homeassistant-inovelli-hue-blueprints&filepath=blueprints/automation/inovelli/hue_dimmer_zha_unified.yaml)

[![Import Blueprint: Script](https://img.shields.io/badge/Home%20Assistant-Import%20Script-blue?logo=home-assistant)](https://my.home-assistant.io/redirect/blueprint_import/?repository_url=https://github.com/Ratoka/homeassistant-inovelli-hue-blueprints&filepath=blueprints/script/inovelli/dim_hue_room_lights.yaml)

# 🏠 Home Assistant Inovelli Hue Blueprints

This repository contains **dynamic, reusable blueprints** for integrating Inovelli Blue Series dimmers (via ZHA) with Philips Hue lights and scenes. These automations are designed for **state-aware, adaptive lighting control** that evolves with your Hue setup.

---

## ✨ Features

- **💡 Light On/Off Control**
  - Single tap up: Turns Hue room **on**
  - Single tap down: Turns Hue room **off**
  - Works regardless of whether lights were last controlled by switch, app, or automation
  - Optional: Automatically activates a default scene when turning on

- **Unified Paddle Dimming**
  - Hold paddle: Smooth dim up/down
  - Release paddle: Stop dimming
  - Uses `input_boolean.dimmer_<room>` to control dimming loop

- **🎬 Scene Cycling (Button 3)**
  - Press: Cycle forward through Hue scenes
  - Hold: Cycle backward
  - Scenes are dynamically discovered per Hue room
  - Tracks state with `input_number.scene_index_<room>`

- **🧼 Clean Entity Naming Convention**
  - `light.<room>` for Hue Room/Zone
  - `input_boolean.dimmer_<room>` for dimming control
  - `input_number.scene_index_<room>` for scene tracking

---

## 🛠️ Requirements

For each room (e.g. `Office`), create:

| Entity | Example | Purpose |
|--------|---------|---------|
| Hue Light Group | `light.office` | Hue Room/Zone |
| Input Boolean | `input_boolean.dimmer_office` | Controls dimming loop |
| Input Number | `input_number.scene_index_office` | Tracks active scene index |
| Hue Scenes | `scene.office_relax`, etc. | Must follow `scene.<room>_<name>` pattern |

---

### 🛠️ Creating inputs

The inputs are used to allow a single automation to trigger on/off, dimming and scene rotations. 
A set of inputs are required per switch/automation.  Depending on your personal preference, 
these can be configured in the UI or via YAML.  Below provides steps for the HA UI.

### 🔘 input_boolean: Toggle Helper

This helper is used to enable or disable specific automations or modes.

**Steps to create:**
1. Go to **Settings > Devices & Services > Helpers**.
2. Click **+ Add Helper**, then select **Toggle**.
3. Set a name like `scene_cycling_enabled` or your preferred label.
4. Optionally set the icon (e.g., `mdi:lightbulb-group`).
5. Click **Create**.

### 🎚️ input_number: Slider or Number Box

Use this helper to store values like the current scene index or delay intervals.

**Steps to create:**
1. Navigate to **Settings > Devices & Services > Helpers**.
2. Click **+ Add Helper**, then choose **Number**.
3. Configure the details:
   - **Name**: e.g., `current_scene_index`
   - **Minimum / Maximum**: Set appropriate range (e.g., 0–10)
   - **Step size**: Set increment (e.g., 1)
   - **Unit of measurement**: Optional (e.g., none or "index")
4. Click **Create**.

### ✅ Tips
- Use the names exactly as defined in your YAML blueprint for seamless automation.
- You can rename or localize labels afterward—entity IDs remain the key reference.

Once created, these helpers will appear under **Developer Tools > States**, and can be referenced directly in your automations or blueprints.


## 📁 Included Blueprints

### 🔧 Hue Paddle Dimming + Scene Cycling (ZHA Event)
- **Path**: `blueprints/automation/inovelli/hue_dimmer_zha_unified.yaml`
- **Handles**:
  - Paddle dimming (start/stop)
  - Scene cycling (forward/back)
  - Light on/off control
  - Default scene activation
  - Detailed logging

### 🎚️ Hue Room Dimmer - Dynamic Up/Down
- **Path**: `blueprints/script/inovelli/dim_hue_room_lights.yaml`
- **Handles**:
  - Smooth dimming loop
  - Customizable brightness step
  - Parameterized by room, direction, and step

---

## 🧪 Example Setup: Room = `Office`

1. In the Hue app, create a room named `Office`
2. In Home Assistant, create the following helpers:
   - `input_boolean.dimmer_office`
   - `input_number.scene_index_office`
3. Add or sync Hue scenes like:
   - `scene.office_relax`
   - `scene.office_energize`
4. Create a script from the **Hue Room Dimmer** blueprint:
   - Set `room` to `Office`
   - Set `direction` to `up` or `down`
   - Set `step` to your preferred brightness increment
5. Create an automation from the **Hue Paddle Dimming + Scene Cycling** blueprint:
   - Set `room` to `Office`
   - Link the dimmer script you created
   - Optionally enable default scene activation

Now your Inovelli switch will:
- Tap up: Turn on `light.office` (and optionally activate a default scene)
- Tap down: Turn off `light.office`
- Hold: Dim up/down smoothly
- Release: Stop dimming
- Button 3 press/hold: Cycle through Hue scenes

---

## 📜 License

See the LICENSE file