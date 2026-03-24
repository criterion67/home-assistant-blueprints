# Home Assistant Blueprints

A collection of reusable blueprints for [Home Assistant](https://www.home-assistant.io/) automations.

---

## Blueprints

### Philips Hue Smart Button (RDM005) - Zigbee2MQTT Fixed

Fixes the broken Zigbee2MQTT action mapping for the **RDM005** hardware revision of the Philips Hue Smart Button. The original EPMatt blueprint used action strings from the older ROM001 revision, causing the button to silently do nothing.

Supports short press, long press with loop-until-release for brightness ramping, button release, and virtual double press.

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/hue_smart_button_rdm005/philips_hue_smart_button_rdm005.yaml)

[Full setup instructions](blueprints/automation/hue_smart_button_rdm005/README.md)

---

### Leak Alert Notification Loop with Siren & TTS

Monitors moisture sensors and alerts you when a leak is detected. Repeats every 5 minutes with TTS announcements, a siren loop, and mobile notifications with working **Snooze** and **Dismiss** buttons.

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/leak_alert_loop/leak_alert_loop.yaml)

[Full setup instructions](blueprints/automation/leak_alert_loop/README.md)
