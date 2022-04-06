# Sowillo IoT Board WiFi Connection HOWTO

This article describes configuring Sowilo Box to be used with the user WiFi network.

Sowillo IoT board comes with a pre-flashed firmware that will connect to
a Sowillo MQTT server.

First, you need to connect your Sowillo IoT board to WiFi. This can be
done via the captive portal in a few steps:

- Wait 1 minute after board power-up and find `"heatmeter_2kb4-******"` WiFi network
- Connect to `"heatmeter_2kb4-******"` with password `"development"`
- Open the SignIn page from Android messages and enter Your
    `"WiFi_SSID_Name"` and `"Password"`, then save settings.
- If You aren't planning re-connect the device to another MQTT cloud service, please - leave unchanged MQTT settings (`Addr`, `Port`, `User`, `Pass`).

<img src="./Pictures/access_point_user_wifi_example.jpg" alt="iot-dashboard" height="600">
![](./Pictures/access_point_user_wifi_example.jpg)