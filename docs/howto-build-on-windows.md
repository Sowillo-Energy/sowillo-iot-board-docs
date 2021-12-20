# How-to guide: Build Sowillo firmware with patched ESPhome on Windows

This document describes how to locally build the latest Sowillo firmware
for the **Sowillo IoT board** on Windows.

Please contact us if you have any questions



##1. Install python

Chose the appropriate python version for your system on
[*python.org*](https://www.python.org/downloads/) and download it.

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/10000201000006490000038D85ABC3E1609F3025.png" style="width: 100%;" alt="iot-dashboard" height="250">

Run the installer.

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100002010000064C0000038F37DD2D958B9AA5D9.png" style="width: 100%;" alt="iot-dashboard" height="250" >

On the first installation dialog select the option `Add Python to
PATH` or `Add Python to environment variables`, this step is
important, so far you will not be able to run `python` from windows
console. If you missed it - you can add it manually later using `System
Utility` in `Control Panel` on your Windows

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100002010000064B00000390C7B4DBF655B7B1D6.png" style="width: 100%;" alt="iot-dashboard" height="250" >

In case if you forgot to add the option `Add Python to PATH` - you
won't be able to run `python` command from your `Windows Command
Prompt`. Instead you will see the message

```command
Python was not found; run without arguments to install from the
Microsoft Store, or disable this shortcut from Settings
```
*Just in this case* do the following steps:

1.  Go to the python installation directory and find there python.exe
    binary. You will need the path to the directory that contains the
    python.exe
2.  Right-click on "This PC\'\' and go to "Properties".

    <img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100000000000019A000001CD05E50336313E2B2A.png" style="width: 100%;" alt="iot-dashboard" height="500" >

1.  Click on the "Advanced system settings" in the menu on the left.
2.  Click on the Environment Variables button o​n the bottom right.
3.  In the System variables section, select the "Path variable" and
    click on "Edit". The next screen will show all the directories that
    are currently a part of the PATH variable.

    <img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/1000000000000209000001F391926BE697AB9056.png" alt="iot-dashboard" height="500" >

1.  Click on New and enter the path to the Python's install directory.

## 2. Download ESPHome:

Download the Sowillo\'s patched ESPHome from [this link](https://rawcontent.sowillo.com/repository/binary-files-ext/latest/esphome-patched.zip).
[**ESPHome**](https://esphome.io/) - is an open-source python package that allows you to build and
flash firmware for `ESP8266`/`ESP32` boards, in our case - `ESP32`. While we
worked on our boards we found some issues in `ESPHome`, but fixes are still
not included to upstream. For now we providing to the user the [patched
version](https://rawcontent.sowillo.com/repository/binary-files-ext/latest/esphome-patched.zip) of ESPHome and looking forward for our changes will be included
to the ESPHome upstream.

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/10000201000006490000038DD294F636B497697A.png" style="width: 100%;" alt="iot-dashboard" height="250" >

## 3. Install ESPHome

Unpack the ESPHome package to some directory. In this tutorial we'll
use the`C:\esphome` path.

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100002010000064A0000038DCE675708FE9E82B1.png" style="width: 100%;" alt="iot-dashboard" height="250" >

Open the Windows Command Prompt and navigate to the esphome directory.
Note: this Command Prompt window must be opened *after* you installed
python, *not before.*

```command
cd \esphome
```

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100002010000064C0000038D8E423BAF1C3731B1.png" style="width: 100%;" alt="iot-dashboard" height="250" >

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/10000201000006490000038E9424F0D234BD1D83.png" style="width: 100%;" alt="iot-dashboard" height="250" >

Now we'll create the python virtualenv for ESPHome. Don't worry, all
further steps will not affect your system.

```command
python -m venv esphome-venv
```

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100002010000064B0000038F188D949EDBE97BF8.png" style="width: 100%;" alt="iot-dashboard" height="250" >

This will create a `esphome-venv` directory inside `esphome` with
python virtual environment. Let's activate it:

```command
.\esphome-venv\Scripts\activate
```

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/10000201000006480000038D0AF8A264E279940D.png" style="width: 100%;" alt="iot-dashboard" height="250" >

You may want to see the environment name at the beginning of the command
prompt.

The next step is to install patched ESPHome package into this virtual
environment:

(This command should be done from the esphome dir, don't forget the dot
at the end)

```command
pip install -e .
```

Flashing dev board under windows requires the cp2102 win driver with
enumerator, which could be downloaded by [*link*](https://www.silabs.com/documents/public/software/CP210x_Windows_Drivers_with_Serial_Enumeration.zip).

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100002010000064B000003904E3378BE99D6EBFA.png" style="width: 100%;" alt="iot-dashboard" height="250" >

## 4. Build firmware

Download the Sowillo's [configuration for the ESPHome](https://rawcontent.sowillo.com/repository/binary-files-ext/latest/sowillo-esphome-configuration.zip).

This archive contains the prepared configurations for the ESPHome.

Unpack the configuration for the ESPHome archive to some directory. In
this tutorial we'll use the `C:\esphome-configuration` path,
you can change it according to your own needs.

*The mandatory step* - is to create the `secrets.yaml` file in the root of the directory.
You can copy it from the `secrets.yaml.in` template and fill it in
`secrets.yaml` file (file extension must be `.yaml`). You may be interested
in wifi `wifi_ssid` and `wifi_password` fields that allow the
board to connect to your wifi. Also you may want to configure
`mqtt_broker` and `mqtt_port` on your mqtt broker.

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100002010000064B0000038C5DEC198220789ACE.png" style="width: 100%;" alt="iot-dashboard" height="250" >

Use the virtual environment that you created in the step above
(esphome-venv). If you already closed the Windows Command Prompt - just
open the new, navigate to the esphome directory and activate it:
```command
cd \esphome
.\esphome-venv\Scripts\activate
```

Now go to the configuration directory:
```command
cd \esphome-configuration
```

Finally you can build the configuration that you want:
```command
esphome swlbox-202-thermostat.yaml compile
```

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/10000201000006470000038A2C5D0AC80C17BF39.png" style="width: 100%;" alt="iot-dashboard" height="250" >

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100002010000064C0000038EF97D5468543750EB.png" style="width: 100%;" alt="iot-dashboard" height="250" >

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100002010000064F0000038EC2D1692DF947BF58.png" style="width: 100%;" alt="iot-dashboard" height="250" >


## 5. Flash firmware

Initiate uploading firmware to ESP32 board with console command:
```compile
esphome swlbox-202-thermostat.yaml compile
```
after checking firmware readiness enter proper COM port connected to
ESP32 board, or choose On-Air updating - if the board was flashed, but
Firmware Over The Air update is necessary:
