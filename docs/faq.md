# FAQ

Questions go to [GitHub issues](https://github.com/MyGrid-Energy/mygrid-homeassistant-mqtt/issues) or [support@mygrid.energy](mailto:support@mygrid.energy).

## Nothing appears in Home Assistant

1. In the MyGrid app, **Features → Home Assistant** is on, settings are applied, and status is **Connected**.
2. Home Assistant’s MQTT integration uses **the same broker** (same IPv4 address and port).
3. MQTT Discovery is enabled (default for the Mosquitto add-on).
4. The broker is on the same LAN. The app asks for a **local IPv4** address (`mqtt://`).

## Power Setpoint is missing or greyed out

**Enable Home Assistant** only shares diagnostics. The Features screen says so: it does not give Home Assistant control of the battery.

On ModuleTwo, open **Control** and choose **Home Assistant control**. Then the Power Setpoint entity becomes writable. VoltBridge has no setpoint — it is meter data only.

## Power numbers look wrong

Two different units and two different signs:

| Device | Unit | Positive | Negative |
| --- | --- | --- | --- |
| ModuleTwo Power / Power Setpoint | **W** | charging | discharging |
| VoltBridge Actual power | **kW** | import (from the grid) | export (to the grid) |

1 kW on VoltBridge is 1000 W on ModuleTwo. Export on VoltBridge is negative; charging ModuleTwo from that surplus is a **positive** setpoint.

## Home Assistant or the broker stopped and the battery is still charging or discharging

Expected on ModuleTwo under **Home Assistant control**: the last setpoint is held. Safety on the battery still applies. Choose **MyGrid Smart Control** to return to automatic.

## Energy dashboard shows little or nothing

See [Energy dashboard](energy-dashboard.md). Use VoltBridge **kWh totals** (not instantaneous kW) as grid sensors, and ModuleTwo **Energy Charged / Energy Discharged** as the battery.
