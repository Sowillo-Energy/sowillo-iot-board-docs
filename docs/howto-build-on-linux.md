# How-to guide: Build Sowillo firmware with patched ESPHome on Linux

This tutorial describes how to build the firmware for sowillo box on Linux. All steps made on clean [Ubuntu 20.04](https://ubuntu.com/download).

<img src="https://raw.githubusercontent.com/Sowillo-Energy/sowillo-iot-board-docs/main/docs/Pictures/100000000000077E0000041B30F3830C2C626DB0.png" alt="iot-dashboard" height="500"/>

Update cache and install dependencies:

```bash
sudo apt update
sudo apt install python3 unzip python3-venv
```
Create a separate directory for build:
```bash
mkdir build-sowillo && cd build-sowillo
```
Download and unzip latest patched ESPHome package:
```bash
wget \
https://rawcontent.sowillo.com/repository/binary-files-ext/latest/esphome-patched.zip
mkdir esphome-patched && unzip esphome-patched.zip -d esphome-patched
```
Download and unzip latest ESPHome configurations for **Sowillo IoT Board**:
```bash
wget \
https://rawcontent.sowillo.com/repository/binary-files-ext/latest/sowillo-esphome-configuration.zip

mkdir sowillo-esphome-configuration && unzip
sowillo-esphome-configuration.zip -d sowillo-esphome-configuration
```
Create a python virtual environment, activate it and install patched esphome to the environment:
```bash
python3 -m venv esphome-venv
source esphome-venv/bin/activate
pip install -U pip
pip install -e esphome-patched
```
Build firmware:
```bash
cd sowillo-esphome-configuration
mv secrets.yaml.in secrets.yaml
```
Edit `secrets.yaml`, you may configure your default WiFi settings and MQTT broker settings there:
```bash
nano secrets.yaml
```
Build the firmware that you're interested in:
```bash
esphome compile swlbox-300.yaml
```
