# Home Assistant Blueprints

A collection of reusable blueprints for [Home Assistant](https://www.home-assistant.io) automations.

---

## 🚨 Leak Alert Notification Loop with Siren & TTS

When a leak is detected, this automation:
- Announces the leak using text-to-speech (TTS)
- Sends a mobile app notification with **Snooze** and **Dismiss**
- Sounds a siren (8s on / 12s off) for 1 minute
- Repeats every 5 minutes until the leak is dismissed or cleared

---

### 🧩 Import Blueprint

Click the button below to import this blueprint directly into Home Assistant:

[![Open in Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?repository_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/leak_alert_loop/leak_alert_loop.yaml)

Or use this raw URL:
https://raw.githubusercontent.com/criterion67/home-assistant-blueprints/main/blueprints/automation/leak_alert_loop/leak_alert_loop.yaml
---

### 🔧 Requirements

- Leak sensors (`binary_sensor` with `device_class: moisture`)
- alias: Leak Alert - Snooze Handler
trigger:
  - platform: event
    event_type: mobile_app_notification_action
    event_data:
      action: SNOOZE_LEAK
action:
  - service: input_boolean.turn_on
    target:
      entity_id: input_boolean.leak_alert_snoozed
mode: single
- Siren switch (e.g., smart plug or relay)
- Media player for announcements
- Mobile app integration
- Input boolean to track snooze

Example name map:
```yaml
{
  "binary_sensor.kitchen_leak_sensor_2_moisture": "Kitchen Sink",
  "binary_sensor.hvac_condensate_pan_sensor_9": "HVAC Pan"
}
alias: Leak Alert - Dismiss Handler
trigger:
  - platform: event
    event_type: mobile_app_notification_action
    event_data:
      action: DISMISS_LEAK
action:
  - service: input_boolean.turn_off
    target:
      entity_id: input_boolean.leak_alert_snoozed
mode: single
