# 🧾 Changelog

All notable changes to this project will be documented in this file, following [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format.

---

## [0.1.1] - 2025-06-29

### Added
- Visual setup diagram illustrating integration between Hue, ZHA-based Inovelli Blue switches, and Home Assistant helpers.
- Added troubleshooting info to the README documenting debug log examples and helper usage.
- Scene cycling automation with dynamic scene discovery using `input_number.scene_index_<room>`.
- Paddle dimming functionality via `input_boolean.dimmer_<room>` and `dim_hue_room_lights.yaml` script.
- Support for directional hold (up/down) with brightness adjustment logic.
- YAML templates referencing `room_slug` to standardize helper and scene naming.

### Changed
- Updated debug logs to standardize format and include helper states, active scenes, and light modes (e.g. `xy_color`).
- README enhancements to clarify helper setup and event mapping.

### Fixed
- Color mismatch between identical Hue bulbs by preferring `xy_color` mode in automations.
- Scene restoration logic to better preserve original color temperature vs color mode.

### Deprecated
- Manual scene list definitions — replaced with dynamic discovery via templates.

---

## [0.1.0] - 2025-06-29

Initial release of:
- Dimmer automation blueprint
- Scene cycler blueprint
- Light level script

Includes basic README and prerequisites checklist.
