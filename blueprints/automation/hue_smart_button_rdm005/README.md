# Philips Hue Smart Button (RDM005) - Home Assistant Blueprint

A Home Assistant automation blueprint for the **Philips Hue Smart Button (RDM005)** via **Zigbee2MQTT**.

This is a fixed fork of the excellent [Awesome HA Blueprints](https://github.com/EPMatt/awesome-ha-blueprints) project by EPMatt. The original blueprint used Zigbee2MQTT action strings from the older **ROM001** hardware revision of this button. The **RDM005** sends completely different action strings, causing the automation to silently do nothing on every button press.

---

## The Bug (and the Fix)

| Event | ROM001 (original - broken) | RDM005 (this fix - correct) |
|---|---|---|
| Short press | `press` | `on` |
| Long press / hold | `hold` | `brightness_move_up` |
| Release | `release` | `brightness_stop` |

---

## Requirements

- Home Assistant 2024.10.0 or newer
- Zigbee2MQTT integration
- Philips Hue Smart Button **RDM005** (product code 8718699693985) paired to Z2M
- One `input_text` helper entity (max length 255)

---

## Import Blueprint

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/hue_smart_button_rdm005/philips_hue_smart_button_rdm005.yaml)

Or paste this URL directly into **Settings → Automations & Scenes → Blueprints → Import Blueprint**:

```
https://raw.githubusercontent.com/criterion67/home-assistant-blueprints/main/blueprints/automation/hue_smart_button_rdm005/philips_hue_smart_button_rdm005.yaml
```

---

## Setup

1. Create an `input_text` helper — **Settings → Devices & Services → Helpers → Create Helper → Text**, max length **255**
2. Go to **Settings → Automations & Scenes → Blueprints**, find this blueprint, click **Create Automation**
3. Configure:

| Input | Value |
|---|---|
| Controller Device | Your Hue Button from the dropdown |
| Helper - Last Controller Event | Your `input_text` helper |
| Button short press | e.g. `light.toggle` |
| Button long press | e.g. `light.turn_on` with `brightness_step_pct: 15` |
| Button long press - loop until release | Enable for smooth ramping |
| Button release | Optional action on release |
| Virtual double press | Optional second action |

---

## Example: Toggle + Brightness Ramp

- **Short press** → `light.toggle`
- **Long press** → `light.turn_on` with `brightness_step_pct: 15`, `transition: 0.2`
- **Loop until release** → enabled
- **Max loop repeats** → 20

---

## Credits

Based on the original [Controller - Philips 8718699693985 Hue Smart Button](https://github.com/EPMatt/awesome-ha-blueprints) blueprint by [EPMatt (Matteo Agnoletto)](https://github.com/EPMatt). Fixed Z2M action mapping for RDM005 hardware revision.
