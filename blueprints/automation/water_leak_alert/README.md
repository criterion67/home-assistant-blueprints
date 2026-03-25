# Water Leak Alert - Blueprint Set

A Home Assistant 3-blueprint set. TTS announcements, persistent mobile notifications with working Snooze and Dismiss, and pulsing siren. Repeats every 5 min until dismissed. Based on real production automations.

---

## Requirements

Two input_boolean helpers (Settings > Devices & Services > Helpers > Toggle):

| Helper | Suggested Name |
|---|---|
| Snooze | input_boolean.leak_alert_snoozed |
| Dismiss | input_boolean.leak_alert_dismissed |

---

## Blueprint 1 - Triggered Response

[![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/water_leak_alert/water_leak_alert_triggered_response.yaml)

Inputs: Leak Sensors, Siren Switch, TTS Service, Media Player, Notification Service, Snooze Boolean, Dismiss Boolean

---

## Blueprint 2 - Snooze Handler

[![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/water_leak_alert/water_leak_alert_snooze_handler.yaml)

Input: Snooze Boolean (must match Blueprint 1)

---

## Blueprint 3 - Dismiss Handler

[![Import](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/water_leak_alert/water_leak_alert_dismiss_handler.yaml)

Input: Dismiss Boolean (must match Blueprint 1)
