# Leak Alert Notification Loop with Siren & TTS

A Home Assistant blueprint that monitors moisture sensors and alerts you when a leak is detected. Repeats every 5 minutes with TTS announcements, a siren loop, and mobile notifications until you Snooze or Dismiss.

---

## What It Does

When a leak is detected:
1. Announces the alert via TTS on a media player
2. Sends a mobile notification with **Snooze** and **Dismiss** action buttons
3. Triggers a siren loop (3 cycles of 8s on / 12s off)
4. Waits 5 minutes and repeats

**Snooze** pauses alerting for 5 minutes then resumes automatically.
**Dismiss** stops all alerting until the sensor resets and triggers again.

---

## Requirements

Before setting up the blueprint, create these helpers in **Settings > Devices & Services > Helpers**:

| Helper | Type | Purpose |
|---|---|---|
| e.g. `input_boolean.leak_snooze` | Toggle (input_boolean) | Tracks snooze state |
| e.g. `input_boolean.leak_dismiss` | Toggle (input_boolean) | Tracks dismiss state |

Both helpers should start with their initial state set to **off**.

---

## Import Blueprint

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/leak_alert_loop/leak_alert_loop.yaml)

Or paste this URL directly into **Settings > Automations & Scenes > Blueprints > Import Blueprint**:

```
https://raw.githubusercontent.com/criterion67/home-assistant-blueprints/main/blueprints/automation/leak_alert_loop/leak_alert_loop.yaml
```

---

## Setup

After importing:

1. Go to **Settings > Automations & Scenes > Blueprints**
2. Find **Leak Alert Notification Loop with Siren & TTS** and click **Create Automation**
3. Fill in the inputs:

| Input | Description | Example |
|---|---|---|
| Leak Sensors | One or more moisture binary sensors | `binary_sensor.kitchen_leak` |
| Siren Switch | Switch entity to use as siren | `switch.siren` |
| TTS Service | Your TTS service name | `tts.home_assistant_cloud` or `tts.google_translate_say` |
| Media Player for TTS | Where to announce | `media_player.living_room` |
| Mobile Notification Service | Your notify service | `notify.mobile_app_my_phone` |
| Snooze Input Boolean | Helper created above | `input_boolean.leak_snooze` |
| Dismiss Input Boolean | Helper created above | `input_boolean.leak_dismiss` |

4. Save the automation.

---

## TTS Service Options

| Service | Requires | Notes |
|---|---|---|
| `tts.home_assistant_cloud` | Nabu Casa subscription | Best voice quality |
| `tts.google_translate_say` | Nothing | Free, requires internet |
| `tts.piper` | Piper add-on | Free, fully local |

---

## Finding Your Notification Service

Your mobile notification service name follows the pattern `notify.mobile_app_DEVICENAME`.

To find it: **Settings > Devices & Services > Integrations > Mobile App** — your device name is shown there. Replace spaces with underscores and lowercase everything.

Example: Device named "Scott's Phone" becomes `notify.mobile_app_scotts_phone`

---

## What Changed in v2 (Bug Fixes)

If you used the original version of this blueprint, here is what was fixed:

- **While loop logic** - The original loop condition was broken and could run indefinitely or stop prematurely
- **Snooze/Dismiss buttons** - The original notification buttons did nothing when tapped; they now actually pause or stop the alert
- **Deprecated service syntax** - Updated from deprecated `service:` template syntax to current `action:` syntax
- **Hardcoded TTS** - TTS service is now a configurable input instead of hardcoded to Nabu Casa
- **New dismiss helper required** - A second `input_boolean` is now needed for dismiss state (the original only required one)

---

## Changelog

**v2** - Fixed while loop, snooze/dismiss handling, deprecated service syntax, TTS flexibility
**v1** - Initial release
