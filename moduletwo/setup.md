# Setup

You need a Home Assistant MQTT broker on the same network as ModuleTwo (the Mosquitto add-on is typical). ModuleTwo speaks **MQTT** (`mqtt://`) on that LAN. The same broker fields are used for [VoltBridge](../voltbridge/).

## 1. Broker in the MyGrid app

Open the device → **Features → Home Assistant**.

![Enable Home Assistant and MQTT broker](../images/app-features-home-assistant.png)

The app copy is explicit: **diagnostics only** — this toggle does not give Home Assistant control of the battery.

| Field | What to enter |
| --- | --- |
| Protocol | `mqtt://` (fixed in the app) |
| Host | Local **IPv4** address of the broker |
| Port | Default **1883** |
| Username / password | Optional |

Turn **Enable Home Assistant** on, then **Apply settings**. On success the app shows **Connected**.

The broker settings stay on the device. After **Connected**, Home Assistant telemetry keeps working if your internet connection drops.

## 2. Let entities appear

Home Assistant uses MQTT Discovery. You do not add YAML for ModuleTwo. After **Connected**, a device named after ModuleTwo and its device id should show up under MQTT devices.

If it does not, see the [FAQ](../docs/faq.md).

## 3. Hand over control (optional)

Open **Control** (available when Home Assistant is **Connected**). Under **Choose battery control**:

![Home Assistant control](../images/app-control-home-assistant.png)

- **Home Assistant control** — the Power Setpoint entity in Home Assistant becomes writable. The app shows the battery as controlled externally.
- **MyGrid Smart Control** — ModuleTwo takes automatic control again. The Power Setpoint entity becomes unavailable. Strategy changes stay here.

See [control.md](control.md) for what happens on that switch and if Home Assistant stops.

## 4. Energy dashboard (optional)

See [Energy dashboard](../docs/energy-dashboard.md). Use **Energy Charged** and **Energy Discharged** as the battery.
