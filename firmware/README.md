# Installing in HA

I have a created a private repository for myself for all my esphome configs, the files in this repo can be considered templates as such. I describe the steps you can take to create a similar setup.

1. Copy the contents of this dir to a repository you can commit to.
1. Rename and change the `iaq-roomname.yaml` to your situation. In case you have more iaq boards make copies of this file and change accordingly.
1. Install the ESPHOME add-on
1. Checkout this repo in your HA installation so that the root is in `/config/esphome/`
1. Make sure the following secrets are set in your `/config/secrets.yaml` (so not the `secrets.yaml`'s in this repo, those are just including the `secrets.yaml` one dir above.
  - `wifi_iot_ssid`
  - `wifi_iot_password`
  - `ap_fallback_hotspot_password`
  - `encryption_key`
  - `ota_password`
1. The first time you cannot flash OTA, so consult the esphome documentation to flash the ESP32 while plugged in. I was not able to flash my wemos d1 esp32 while plugged in to the iaq pcd, so disconnect from that if this is also the case for you. It is able to receive OTA updates while plugged in.


# Firmware

Firmware is created with [ESPHome](https://esphome.io/index.html) -  it is a system to control your ESP8266/ESP32 by simple yet powerful configuration files and control them remotely through Home Automation systems.

I am not going to explain in details [the configuration yaml file.](iaq_board.yaml) If you want to modify it, you need to get familiar with esphome. The config file is fairly complicated compared with the usual esphome configurations, so there is some steeper learning curve, especially if you never programmed an MCU before. However by using esphome, you can build very complex logic without writing a single line of code, as the whole instruction is in the yaml config file. It's amazing how much time it saves!

- [`iaq_board.yaml`](iaq_board.yaml) - this is the configuration for esphome
- [`iaq_board.bin`](iaq_board.bin) - this is the binary file of the compiled firmware and can be directly uploaded in the MCU

## How to flash (or program) the controller?
1. Download [the bin file](iaq_board.bin) on your PC.
2. Install [esphome-flasher](https://github.com/esphome/esphome-flasher).
3. Connect the MCU board with mini USB cable not yet connecting it on PCB.
4. Start esphome-flasher, select the correct COM port which is the MCU as [explained here](https://esphome.io/guides/faq.html#i-can-t-get-flashing-over-usb-to-work) and flash it.

***That's it! Connect the MCU on the board, then power it on and it should work.***

If you want to go deeper, [follow the instructions](https://esphome.io/guides/getting_started_command_line.html) how to build the binary file from the yaml and upload it to the MCU from command line.

# Changelog
###  yaml 1.1.3 / 21 Mar 2021
- update esphome to 1.16.2
- default brightness correction set to +15%
