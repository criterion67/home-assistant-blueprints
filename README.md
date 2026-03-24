# Home Assistant Blueprints

A collection of reusable blueprints for [Home Assistant](https://www.home-assistant.io/) automations.

---

## 🔵 Philips Hue Smart Button (RDM005) - Zigbee2MQTT Fixed

Fixes the broken Z2M action mapping for the RDM005 hardware revision of the Philips Hue Smart Button. Supports short press, long press with loop-until-release for brightness ramping, button release, and virtual double press.

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/hue_smart_button_rdm005/philips_hue_smart_button_rdm005.yaml)

Or use this raw URL:
`https://raw.githubusercontent.com/criterion67/home-assistant-blueprints/main/blueprints/automation/hue_smart_button_rdm005/philips_hue_smart_button_rdm005.yaml`

[View blueprint folder](blueprints/automation/hue_smart_button_rdm005/)

---

## 🚨 Leak Alert Notification Loop with Siren & TTS

When a leak is detected, this automation:
- Announces the leak using text-to-speech (TTS)
- Sends a mobile app notification with **Snooze** and **Dismiss**
- Sounds a siren (8s on / 12s off) for 1 minute
- Repeats every 5 minutes until the leak is dismissed or cleared

### Import Blueprint

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/leak_alert_loop/leak_alert_loop.yaml)

Or use this raw URL: `https://raw.githubusercontent.com/criterion67/home-assistant-blueprints/main/blueprints/automation/leak_alert_loop/leak_alert_loop.yaml`
