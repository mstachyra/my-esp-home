# my-esp-home
Repository for my `esphome` definitions in `yaml`

## Prerequisites

To build and run this yaml files you have to get some knowladge about [ESPHome](https://esphome.io) and device like ESP8266/ESP32

## Setup

Add ignored file `secrets.yaml` in src folder. This will be user for substitutions in `common-esp12e.yaml` file.

``` yaml
ap_password: "AccessPointPassword"
wifi_ssid: "YourWIFI_SSID"
wifi_ssid2: "YourWIFI_Second_SSID"
wifi_password: "YourWIFI_PASS"
```

## ESPHome commands

Just run for example this command.
You have to be in `src` catalog.

``` ps
esphome compile .\s001-3switch.yaml
```

Or other commands from `esphome` cli

```
esphome --help
usage: esphome [-h] [-v] [-q] [-s key value] command ...

positional arguments:
  command               Command to run:
    config              Validate the configuration and spit it out.
    compile             Read the configuration and compile a program.
    upload              Validate the configuration and upload the latest binary.
    logs                Validate the configuration and show all logs.
    discover            Validate the configuration and show all discovered devices.
    run                 Validate the configuration, create a binary, upload it, and start logs.
    clean-mqtt          Helper to clear retained messages from an MQTT topic.
    wizard              A helpful setup wizard that will guide you through setting up ESPHome.
    mqtt-fingerprint    Get the SSL fingerprint from a MQTT broker.
    version             Print the ESPHome version and exit.
    clean               Delete all temporary build files.
    dashboard           Create a simple web server for a dashboard.
    rename              Rename a device in YAML, compile the binary and upload it.
```

## ESP8266 Pinouts

| Label | GPIO   | Input         | Output                | Notes                                                            |
|-------|--------|---------------|-----------------------|------------------------------------------------------------------|
| D0    | GPIO16 | no interrupt  | no PWM or I2C support | HIGH at boot used to wake up from deep sleep                     |
| `D1`    | `GPIO5`  | OK            | OK                    | often used as SCL (`I2C`)                                          |
| `D2`    | `GPIO4`  | OK            | OK                    | often used as SDA (`I2C`)                                          |
| D3    | GPIO0  | pulled up     | OK                    | connected to FLASH button, boot fails if pulled LOW              |
| D4    | GPIO2  | pulled up     | OK                    | HIGH at boot connected to `on-board LED`, boot fails if pulled LOW |
| `D5`    | `GPIO14` | OK            | OK                    | SPI (SCLK)                                                       |
| `D6`    | `GPIO12` | OK            | OK                    | SPI (MISO)                                                       |
| `D7`    | `GPIO13` | OK            | OK                    | SPI (MOSI)                                                       |
| `D8`    | `GPIO15` | pulled to GND | OK                    | SPI (CS) Boot fails if pulled HIGH                               |
| RX    | GPIO3  | OK            | RX pin                | HIGH at boot                                                     |
| TX    | GPIO1  | TX pin        | OK                    | HIGH at boot debug output at boot, boot fails if pulled LOW      |
| `A0`    | `ADC0`   | Analog Input  | X                     |                                                                  |

## Resources

* [Getting Started with the ESPHome](https://esphome.io/guides/getting_started_command_line) 
* [Installing ESPHome Manually](https://esphome.io/guides/installing_esphome.html)