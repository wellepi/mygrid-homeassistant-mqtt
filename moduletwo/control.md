# Control

**Enable Home Assistant** on **Features** only shares diagnostics. Charge and discharge from Home Assistant need **Control**.

## Control in the MyGrid app

**Control → Choose battery control** (when Home Assistant is **Connected**):

![Choose battery control](../images/app-control-home-assistant.png)

| Choice | Who drives the battery |
| --- | --- |
| **MyGrid Smart Control** | ModuleTwo automatic control. Power Setpoint in Home Assistant is unavailable. Strategy changes stay in the app. |
| **Home Assistant control** | Home Assistant may write Power Setpoint. The app shows the battery as controlled externally. |

Switching either way idles the battery (setpoint **0 W**), then the new side takes over. Switch back to **MyGrid Smart Control** when you want automatic operation again.

Restart stays available in Home Assistant in both modes.

## Power Setpoint

Same sign as live Power: **+ charge**, **− discharge**, **0 idle**.

| Direction | Default | Notes |
| --- | --- | --- |
| Charge | up to **+1200 W** | |
| Discharge | up to **−800 W** | Up to **−1200 W** if ModuleTwo is on its own breaker |

Home Assistant shows a number entity with 50 W steps. ModuleTwo applies its own limits as well.

Writes stay on the device across a reboot while you remain on **Home Assistant control**.

## If Home Assistant or the broker stops

ModuleTwo **keeps the last setpoint** (charge or discharge) until the battery is full or empty, or you change Control in the app.

Battery **safety features still apply**: unsafe or out-of-range values are limited, and the pack stays protected if Home Assistant disappears or sends nonsense.

To return to automatic behaviour, set Control to **MyGrid Smart Control**.
