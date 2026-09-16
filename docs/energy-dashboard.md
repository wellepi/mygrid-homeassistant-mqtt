# Energy dashboard

Home Assistant’s [Energy dashboard](https://www.home-assistant.io/docs/energy/) wants lifetime energy (kWh or Wh), not instantaneous power.

## Grid (VoltBridge)

In **Settings → Dashboards → Energy → Electricity grid**, add:

| Flow | VoltBridge entity | Unit |
| --- | --- | --- |
| Grid consumption | **Total consumption** | kWh |
| Return to grid | **Total production** | kWh |

Those are T1+T2 sums. Use the T1/T2 entities only if you want a day/night split.

Do **not** use **Actual power** (kW, net, about once a minute) as a grid energy sensor.

If the meter includes gas, add **Gas consumption** (m³) under Gas.

## Battery (ModuleTwo)

In **Energy → Home battery storage**, add:

| Flow | ModuleTwo entity | Unit |
| --- | --- | --- |
| Energy going into the battery | **Energy Charged** | Wh |
| Energy coming out of the battery | **Energy Discharged** | Wh |

Home Assistant accepts Wh for these counters (`total_increasing`).

You can run the Energy dashboard with only VoltBridge, only ModuleTwo, or both. Both together is the usual household picture: grid from the P1 meter, battery from ModuleTwo.
