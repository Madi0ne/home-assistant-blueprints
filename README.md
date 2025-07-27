# 📘 Philips Hue Dimmer (Multi-Press + Hold) – Z2M Blueprint

This [Home Assistant](https://www.home-assistant.io) automation blueprint provides advanced control for the **Philips Hue Dimmer Switch (324131092621)** when connected via **Zigbee2MQTT**.

It supports:
- ✅ Short Single, Double, and Triple Presses
- ✅ Long Press and Hold Release actions
- ✅ All 4 buttons: `ON`, `OFF`, `UP`, and `DOWN`

## 📦 Features

- Reacts to `_press_release` events to **accurately detect short vs long presses**
- Avoids false triggers from hold
- Supports **multi-press detection** with configurable timeout
- Optional actions: configure only the buttons you use
- Easy to customize via UI or YAML

## 🔧 Requirements

1. **Zigbee2MQTT** integration with your Hue Dimmer switch.
2. Two helpers:
   - `input_number.hue_press_counter`
   - `input_text.mbds1_text_helper`

3. Save this blueprint to:

```
blueprints/automation/Madi0ne/philips_hue_dimmer_z2m.yaml
```

## ⚙️ Blueprint Inputs

| Input | Description |
|-------|-------------|
| `mqtt_action_topic` | Zigbee2MQTT action topic for the device (e.g. `zigbee2mqtt/MBDS1/action`) |
| `press_counter` | An `input_number` helper to store press count |
| `press_state` | An `input_text` helper to track button state (e.g. `idle`, `hold`, `waiting`) |
| `multi_press_delay` | Detection window for double/triple press (in ms) |

### Button Action Inputs

Each button (`on`, `up`, `down`, `off`) supports the following actions:

- Short Single Press
- Short Double Press
- Short Triple Press
- Long Press

All actions are optional – configure only what you need.

## 🧪 Example Use

You can create an automation based on this blueprint like:

```yaml
alias: "Toggle Lamp with Double ON Press"
use_blueprint:
  path: your_username/philips_hue_dimmer_z2m.yaml
  input:
    mqtt_action_topic: zigbee2mqtt/MBDS1/action
    press_counter: input_number.hue_press_counter
    press_state: input_text.mbds1_text_helper
    on_press_2:
      - service: light.toggle
        target:
          entity_id: light.living_room_lamp
```

## 🙌 Credits

Created with ❤️ by [Your Name or GitHub Username]. Inspired by the EPMatt Awesome HA Blueprints.

---

> 💡 Questions or improvements? Submit an issue or PR!
