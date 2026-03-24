# Medication Reminder - Notifications with Snooze

A Home Assistant blueprint set that sends persistent mobile notifications at up to 6 scheduled
medication times per day. Each notification has a **Taken** button and a **Snooze** button.
Tapping Taken clears the notification. Tapping Snooze re-sends it after a configurable delay.

This is a **two-blueprint set** - you need to import and configure both.

---

## How It Works

1. At each scheduled time, a persistent notification is sent to your phone
2. The notification shows the medication title, list, and any notes you configured
3. Tap **Taken** to dismiss the notification silently
4. Tap **Snooze** to dismiss it and receive it again after your configured delay (default 30 min)
5. Snoozed reminders are handled via an `input_boolean` snooze helper per slot

---

## Requirements

Before importing, create one `input_boolean` helper **per active time slot** in
**Settings > Devices & Services > Helpers > Create Helper > Toggle**.

| Slot | Suggested Helper Name |
|---|---|
| Slot 1 | `input_boolean.med_snooze_slot1` |
| Slot 2 | `input_boolean.med_snooze_slot2` |
| Slot 3 | `input_boolean.med_snooze_slot3` |
| Slot 4 | `input_boolean.med_snooze_slot4` |
| Slot 5 | `input_boolean.med_snooze_slot5` |
| Slot 6 | `input_boolean.med_snooze_slot6` |

You only need to create helpers for slots you plan to use. All helpers should start with their initial state set to **off**.

---

## Step 1 - Import the Notifications Blueprint

[![Import Notifications Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/medication_reminder/medication_reminder_notifications.yaml)

Or paste into **Settings > Automations & Scenes > Blueprints > Import Blueprint**:
```
https://raw.githubusercontent.com/criterion67/home-assistant-blueprints/main/blueprints/automation/medication_reminder/medication_reminder_notifications.yaml
```

## Step 2 - Import the Actions Blueprint

[![Import Actions Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/criterion67/home-assistant-blueprints/blob/main/blueprints/automation/medication_reminder/medication_reminder_actions.yaml)

Or paste into **Settings > Automations & Scenes > Blueprints > Import Blueprint**:
```
https://raw.githubusercontent.com/criterion67/home-assistant-blueprints/main/blueprints/automation/medication_reminder/medication_reminder_actions.yaml
```

---

## Step 3 - Configure the Notifications Automation

Go to **Settings > Automations & Scenes > Blueprints**, find
**Medication Reminder - Notifications with Snooze** and click **Create Automation**.

| Input | Description | Example |
|---|---|---|
| Mobile Notification Service | Your phone's notify service | `notify.mobile_app_my_phone` |
| Snooze Duration | Minutes before re-sending after snooze | `30` |
| Slot 1 - Enable | Turn this slot on | ✅ |
| Slot 1 - Time | When to send the reminder | `07:00:00` |
| Slot 1 - Title | Notification title | `💊 7:00 AM Medications` |
| Slot 1 - Message | Medications and notes | `Levothyroxine 100mcg - take on empty stomach` |
| Slot 1 - Snooze Helper | The helper you created | `input_boolean.med_snooze_slot1` |

Repeat for each slot you need (up to 6). Leave unused slots disabled.

---

## Step 4 - Configure the Actions Automation

Go to **Settings > Automations & Scenes > Blueprints**, find
**Medication Reminder - Handle Notification Actions** and click **Create Automation**.

Use the **exact same** notification service and snooze helpers as you configured in Step 3.
Enable only the slots you enabled in Step 3.

---

## Finding Your Notification Service

Your service follows the pattern `notify.mobile_app_DEVICENAME`.

To find it: **Settings > Devices & Services > Integrations > Mobile App**.
Your device name is shown there. Replace spaces with underscores and lowercase everything.

Example: Device named "My Pixel 9" becomes `notify.mobile_app_my_pixel_9`

---

## Tips

- The message field supports newlines - list each medication on its own line for clarity
- Add timing notes (e.g. "take with food", "empty stomach") directly in the message
- If you have medications that are only taken on certain days, use the standard HA condition
  editor after creating the automation and taking control of it
- All 6 slots share the same snooze duration - if you need different durations per slot,
  create separate automation pairs from the blueprints

---

## Changelog

**v1** - Initial release. Up to 6 configurable time slots, persistent notifications,
working Taken and Snooze buttons, configurable snooze delay.
