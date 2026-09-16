# Entities and MQTT topics

`{id}` is the ModuleTwo device id (same id Home Assistant shows on the device).

All entities share one availability topic. When ModuleTwo is connected to the broker it publishes `online`; when it drops, Home Assistant sees `offline`.

**Sign convention** (Power and Power Setpoint): **positive = charging**, **negative = discharging**, **0 = idle**.

## Home Assistant entities

| Name in HA | Role | Unit | Notes |
| --- | --- | --- | --- |
| Power | Live battery power | W | Updates live while connected |
| State of Charge | Battery SoC | % | |
| Stored Energy | Energy currently in the pack | Wh | |
| Energy Discharged | Lifetime discharged | Wh | Energy dashboard (`total_increasing`) |
| Energy Charged | Lifetime charged | Wh | Energy dashboard (`total_increasing`) |
| Restart | Reboot ModuleTwo | — | Always available |
| Power Setpoint | Charge/discharge command | W | Writable only under **Home Assistant control**; otherwise unavailable. 50 W steps. Default **−800 … +1200**. Discharge may extend to **−1200** when ModuleTwo is on its own breaker |

## MQTT topics

State is published under `data/device/{id}/…`. Commands go to `…/set/…`. Discovery configs are under `homeassistant/…/config`.

| Topic | R/W | Payload | Unit |
| --- | --- | --- | --- |
| `data/device/{id}/power` | R | signed number | W |
| `data/device/{id}/soc` | R | 0–100 | % |
| `data/device/{id}/energy_level` | R | number | Wh |
| `data/device/{id}/energy_charged` | R | number | Wh |
| `data/device/{id}/energy_discharged` | R | number | Wh |
| `data/device/{id}/power_setpoint` | R | signed number, or empty if unavailable | W |
| `data/device/{id}/set/power_setpoint` | W | signed number | W |
| `data/device/{id}/set/reboot` | W | any non-empty string | — |
| `data/device/{id}` | R | `online` / `offline` | — |

Discovery examples (entity type + `{id}_{object_id}`):

- `homeassistant/sensor/{id}_power/config`
- `homeassistant/sensor/{id}_soc/config`
- `homeassistant/number/{id}_power_setpoint/config`
- `homeassistant/button/{id}_reboot/config`

You normally never write these by hand. They are listed so a broker log is readable.

Command payloads for Power Setpoint are a numeric string in watts, for example `400` or `-800`.
