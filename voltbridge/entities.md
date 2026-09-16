# Entities and MQTT topics

`{id}` is the VoltBridge device id (same id Home Assistant shows on the device).

All entities share one availability topic. When VoltBridge is connected to the broker it publishes `online`; when it drops, Home Assistant sees `offline`.

**Actual power** is **net** (import minus export), in **kW**: **positive = import** (house drawing from the grid), **negative = export** (feeding in). Totals are separate: consumption and production, each in **kWh**.

Sensors are only published when that value is present in the P1 telegram (for example gas, L2/L3, or Belgian demand).

## Home Assistant entities

| Name in HA | Role | Unit | Notes |
| --- | --- | --- | --- |
| Total consumption T1 | Import tariff 1 | kWh | Lifetime, Energy dashboard |
| Total consumption T2 | Import tariff 2 | kWh | Lifetime, Energy dashboard |
| Total consumption | Import T1+T2 | kWh | Prefer this for the Energy dashboard |
| Total production T1 | Export tariff 1 | kWh | Lifetime |
| Total production T2 | Export tariff 2 | kWh | Lifetime |
| Total production | Export T1+T2 | kWh | Prefer this for the Energy dashboard |
| Electricity meter ID | Meter identifier | — | |
| Tariff period | Day (T1) / Night (T2) | — | |
| Actual power | Net power | kW | + import, − export |
| Actual power L1 / L2 / L3 | Net power per phase | kW | When the meter sends phases |
| Voltage phase L1 / L2 / L3 | Phase voltage | V | When present |
| Current phase L1 / L2 / L3 | Phase current | A | When present |
| Gas consumption | Gas total | m³ | When the meter includes gas |
| Current average demand | Capacity-tariff average | kW | When the meter sends it |
| Maximum demand current month | Capacity-tariff peak this month | kW | When the meter sends it |
| Reboot | Restart VoltBridge | — | |

## MQTT topics

State is published under `data/device/{id}/…`. The reboot command is `…/set/reboot`. Discovery configs are under `homeassistant/…/config`.

| Topic | R/W | Payload | Unit |
| --- | --- | --- | --- |
| `data/device/{id}/cons_t1` | R | number | kWh |
| `data/device/{id}/cons_t2` | R | number | kWh |
| `data/device/{id}/cons` | R | number | kWh |
| `data/device/{id}/prod_t1` | R | number | kWh |
| `data/device/{id}/prod_t2` | R | number | kWh |
| `data/device/{id}/prod` | R | number | kWh |
| `data/device/{id}/meter_id` | R | string | — |
| `data/device/{id}/tariff` | R | `Day (T1)` / `Night (T2)` | — |
| `data/device/{id}/power` | R | signed number | kW |
| `data/device/{id}/power_l1` | R | signed number | kW |
| `data/device/{id}/power_l2` | R | signed number | kW |
| `data/device/{id}/power_l3` | R | signed number | kW |
| `data/device/{id}/v_l1` | R | number | V |
| `data/device/{id}/v_l2` | R | number | V |
| `data/device/{id}/v_l3` | R | number | V |
| `data/device/{id}/a_l1` | R | number | A |
| `data/device/{id}/a_l2` | R | number | A |
| `data/device/{id}/a_l3` | R | number | A |
| `data/device/{id}/gas` | R | number | m³ |
| `data/device/{id}/demand_avg` | R | number | kW |
| `data/device/{id}/demand_max_month` | R | number | kW |
| `data/device/{id}/set/reboot` | W | any non-empty string | — |
| `data/device/{id}` | R | `online` / `offline` | — |

Discovery examples:

- `homeassistant/sensor/{id}_cons/config`
- `homeassistant/sensor/{id}_power/config`
- `homeassistant/button/{id}_reboot/config`
