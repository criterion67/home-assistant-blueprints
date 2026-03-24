# Philips Hue Smart Button (RDM005) - Home Assistant Blueprint

A Home Assistant automation blueprint for the **Philips Hue Smart Button (RDM005)** via **Zigbee2MQTT**.

This is a fixed fork of the excellent [Awesome HA Blueprints](https://github.com/EPMatt/awesome-ha-blueprints) project by EPMatt. The original blueprint used Zigbee2MQTT action strings from the older **ROM001** hardware revision. The **RDM005** sends completely different action strings, causing the automation to silently do nothing on every button press.

---

## The Bug (and the Fix)

| Event | ROM001 (original - broken) | RDM005 (this fix - correct) |
|---|---|---|
| Short press | press | on |
| Long press / hold | hold | brightness_move_up |
| Release | release | brightness_stop |

---

## Requirements

- Home Assistant 2024.10.0 or newer
- Zigbee2MQTT integration
- Philips Hue Smart Button **RDM005** (product code 8718699693985) paired to Z2M
- One input_text helper entity (max length 255)

---

## Installation

Import via Home Assistant Blueprints UI using this URL:

https://raw.githubusercontent.com/criterion67/home-assistant-blueprints/main/blueprints/automation/hue_smart_button_rdm005/philips_hue_smart_button_rdm005.yaml

---

## Setup

1. Create an input_text helper with max length 255
2. Create a new automation from the blueprint
3. Select Zigbee2MQTT as the integration
4. Select your Hue Button device
5. Select the input_text helper
6. Configure your actions for short press, long press, release, and optional double press

---

## Example: Toggle + Brightness Ramp

- **Short press** - light.toggle
- **Long press** - light.turn_on with brightness_step_pct: 15, transition: 0.2
- **Loop until release** - enabled
- **Max loop repeats** - 20

---

## Available Actions

- Button short press
- Button long press (with optional loop until release)
- Button release
- Virtual double press (optional, enable separately)

---

## Credits

Based on the original [Controller - Philips 8718699693985 Hue Smart Button](https://github.com/EPMatt/awesome-ha-blueprints) blueprint by EPMatt (Matteo Agnoletto). Fixed Z2M action mapping for RDM005 hardware revision.
