# Limitations

- **MyGrid VoltBridge** (P1 meter) only. MQTT Discovery on a local `mqtt://` broker.
- **Metrics only.** There is no power setpoint and no Home Assistant control mode.
- Actual power is **net kW** (import minus export), not separate import and export power sensors. Use the kWh totals for bought vs fed-in energy.
- Values typically update about **once a minute**, not every second.
- Optional sensors (gas, extra phases, demand) appear only when the meter puts them in the P1 telegram.
- Broker host/port in the app is `mqtt://` (LAN). Username and password are optional.

For battery charge and discharge from Home Assistant, see [ModuleTwo](../moduletwo/).

This repository documents the public MQTT interface. MyGrid watches [issues](https://github.com/MyGrid-Energy/mygrid-homeassistant-mqtt/issues).
