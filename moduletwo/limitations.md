# Limitations

- **MyGrid ModuleTwo** only, with MQTT Discovery on a local `mqtt://` broker.
- **Features → Home Assistant** is diagnostics only. Charge/discharge from Home Assistant requires **Home Assistant control** on the Control tab.
- Power Setpoint discharge defaults to **800 W**. **1200 W** discharge is for ModuleTwo on its own breaker.
- No command timeout toward idle: the last setpoint is held. Safety on the battery still applies. Use **MyGrid Smart Control** to return to automatic.
- Not exposed today: per-phase power, cell voltages, temperatures, outlet, and strategy/schedule editing from Home Assistant.
- Broker host/port in the app is `mqtt://` (LAN). Username and password are optional.

P1 meter MQTT (data only) is documented under [VoltBridge](../voltbridge/).

This repository documents the public MQTT interface. MyGrid watches [issues](https://github.com/MyGrid-Energy/mygrid-homeassistant-mqtt/issues).
