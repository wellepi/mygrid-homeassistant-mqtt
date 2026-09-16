# Setup

You need a Home Assistant MQTT broker on the same network as VoltBridge (the Mosquitto add-on is typical). VoltBridge speaks **MQTT** (`mqtt://`) on that LAN.

This link is **meter data only**. It does not control a battery. The ModuleTwo Features screen says the same for diagnostics: enabling Home Assistant does not hand over battery control.

## 1. Broker in the MyGrid app

Open the device → **Features → Home Assistant** (same fields as [ModuleTwo](../moduletwo/setup.md)).

| Field | What to enter |
| --- | --- |
| Protocol | `mqtt://` (fixed in the app) |
| Host | Local **IPv4** address of the broker |
| Port | Default **1883** |
| Username / password | Optional |

Turn **Enable Home Assistant** on, then **Apply settings**. On success the app shows **Connected**.

The broker settings stay on the device. After **Connected**, Home Assistant telemetry keeps working if your internet connection drops.

## 2. Let entities appear

Home Assistant uses MQTT Discovery. You do not add YAML for VoltBridge. After **Connected**, a device named after VoltBridge and its device id should show up under MQTT devices.

If it does not, see the [FAQ](../docs/faq.md).

Values update about **once a minute** while the P1 meter is delivering telegrams.

## 3. Energy dashboard (optional)

See [Energy dashboard](../docs/energy-dashboard.md). Prefer **Total consumption** and **Total production** as the electricity grid sensors.
