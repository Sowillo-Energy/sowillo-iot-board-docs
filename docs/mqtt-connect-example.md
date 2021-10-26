# IoT MQTT Panel for Android HOWTO

This article describes configuring Sowilo Box to be used with the IoT
MQTT Panel application with pre-built firmware over a public MQTT server
**test.mosquitto.org**.

**MQTT** is a standard IoT protocol for data exchange between devices. It is
very popular, lightweight, and supports publish/subscribe messaging
model. It is supported in almost every morden IoT product. You can find
more information on
[mosquitto.org](https://mosquitto.org), [hivemq.com](https://www.hivemq.com/).

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100000000000026700000500DBF73483592A62B8.jpg" alt="iot-dashboard-1" height="600" >

Sowillo IoT board comes with a pre-flashed firmware that will connect to
a public MQTT server (default: **test.mosquitto.org**). If you have
different firmware, please download and flash the binary from \<link\>
and flash as described in \<link\>. We provide several variants of
pre-build firmware for common public MQTT servers. After getting some
experience, you are advised to build your custom firmware for usage with
your custom server. Please see \<\...\> when you're ready to dive in.

First, you need to connect your Sowillo IoT board to WiFi. This can be
done via the captive portal in a few steps:

-   Wait 1 minute after board reset and find `SWL_fallback_hotspot` WiFi network
-   Connect to `SWL_fallback_hotspot` with password `development`
-   Open SignIn page from Android messages and enter Your
    `WiFi_SSID_Name` and `Password`, then save settings.

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100000000000026700000500E59A9EBD894C39B7.png" alt="iot-dashboard-2" height="600" >

> **Pro hint:** You may want to connect to the MQTT server test.mosquitto.org and verify that the board sends data by monitoring it with an Android app.

Begin by installing the [*IoT*](https://play.google.com/store/apps/details?id=snr.lab.iotmqttpanel.prod&hl=ru&gl=US) [*MQTT Panel*](https://play.google.com/store/apps/details?id=snr.lab.iotmqttpanel.prod&hl=ru&gl=US) application to your Android phone:
<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100000000000047C0000047C33C19CB7FEF6B8C1.png" alt="iot-dashboard-3" height="300" >

We used this app as an example, you can use any MQTT tool you want, just
search MQTT in Play Market/App Store.

Create a connection to public broker test.mosquitto.org and fill in the
following data:

-   Connection name: `MyTestConnection`
-   Client ID: `MyTestClient`
-   Broker Web/IP address: `test.mosquitto.org`
-   Port number: `1883`
-   Network protocol: `TCP`

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100000000000026700000500FBB34566C5E5039F.png" alt="iot-dashboard-4" height="600" >

Add a new dashboard to the Dashboard list and name it TestBoard.
Then press the `Create` button.

Each example FW uses its own unique six char prefix for state and
command topics based on the last 3 bytes of the individual MAC address
ESP32 board.

For example, a unique MAC address `00:11:22:AA:BB:CC` generates MQTT
topics that look like:

```
energymeter_hw_300-aabbcc/switch/energymeter_hw_300_reboot/state
energymeter_hw_300-aabbcc/switch/energymeter_hw_300_reboot/command
energymeter_hw_300-aabbcc/switch/energymeter_hw_300_relay1/state
energymeter_hw_300-aabbcc/switch/energymeter_hw_300_relay1/command
energymeter_hw_300-aabbcc/switch/energymeter_hw_300_relay2/state
energymeter_hw_300-aabbcc/switch/energymeter_hw_300_relay2/command
energymeter_hw_300-aabbcc/sensor/energymeter_hw_300_temperature_1/state
energymeter_hw_300-aabbcc/sensor/energymeter_hw_300_temperature_2/state
energymeter_hw_300-aabbcc/sensor/energymeter_hw_300_uptime_human_readable/state
energymeter_hw_300-aabbcc/sensor/energymeter_hw_300_current/state
```

> **Note:** You can find this information in the Captive Portal.

You may want to add panels with sensor metrics, and relay controls to
the dashboard just created. You can do it as follows:

Open TestBoard and press the *AddPanel* button.

<img src="https://github.com/Sowillo-Energy/sowillo-iot-board-docs/blob/main/docs/Pictures/10000000000002C6000005DBC75FACAB7C70CC68.png?raw=true" alt="add-a-test-log-panel" height="600">

Select *Text Log* and fill the following fields:
- Panel Name: `Uptime`
- Topic: `energymeter_hw_300-aabbcc/sensor/energymeter_hw_300_uptime_human_readable/state`

<img src="https://github.com/Sowillo-Energy/sowillo-iot-board-docs/blob/main/docs/Pictures/100000000000026700000500B69FC9A39547D08B.png?raw=true" alt="add-a-test-log-panel-2" height="600">

In addition to the *TextLog*, there are *Switch, Vertical Meter, Gauge*,
and many other panes for commonly used sensor and switch types.

Other panels could be added in a similar way:

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/1000000000000267000005003044CCD7F334A4C3.png" alt="add-a-test-log-panel-3" height="600">
<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100000000000026700000500DAF0831C182CF480.png" alt="add-a-test-log-panel-4" height="600">
<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/10000000000002670000050010DC28BB64FAFDF1.png" alt="add-a-test-log-panel-5" height="600">
<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/1000000000000267000005009475DBCB1382EECB.png" alt="add-a-test-log-panel-6" height="600">

The final dashboard has the following look:

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/10000000000002670000050062D7FB7C13D9247E.png" alt="add-a-test-log-panel-7" height="600">
