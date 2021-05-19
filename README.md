# eBUS control for home automation

I tested on a Vaillant multiMATIC VRC 700/6 with openHAB.

__Overview:__
 <!--* [Introduction](#introduction)-->
 * [What You Need](#what-you-need)
 * [Setup](#setup)
 * [Alternatives](#alternatives)
 * [References](#references)

<!--## Introduction-->

## What You Need

- **eBUS Adapter**
- Connection to the ebusd
  - [**NodeMCU**](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e5/Nodemcu_amica_bot_02.png/640px-Nodemcu_amica_bot_02.png) (or similar ESP8266 or ESP32-based hardware, like Wemos Lolin32/Wemos D1; the NodeMCU firmware is *not* required) *or*
  - Alternative [hardware](https://github.com/john30/ebusd/wiki/6.-Hardware)
- [**openHAB server**](https://www.openhab.org/docs/installation/)

eBUS adapter (example, my own layout):  
![eBUS Adapter](doc/images/eBUS-Adapter_GH.jpg?raw=true)

## Setup

* Setup openHAB [[Setup instructions](https://www.openhab.org/docs/installation/)]
* Connect eBUS
  * Flash [ebusd-esp](https://github.com/john30/ebusd-esp) to NodeMCU
  * Connect Vcc and GND
  * Connect eBUS adapter Rx to NodeMCU Tx and Tx to Rx
  * Configure the adapter and connect it to the W-LAN
* Install eBUS binding [[Instructions](https://github.com/csowada/openhab2-addons/blob/ebus2x/bundles/org.openhab.binding.ebus/README.md)] [[Releases](https://github.com/csowada/openhab-ebus-binding/releases)]
* [Install](https://github.com/john30/ebusd) and run ebusd (can be run on the same device used for openHAB) and connect to ebusd-esp

**ebusd-esp configuration:**
"direct RX+TX (GPIO3+1)"

**Start eBUS daemon:**
```bash
$ ebusd -d 192.168.1.42:9999 --enablehex --scanconfig= -f -p 8888
[...]
[bus notice] signal acquired
[...]
```

**eBUS binding configuration:** 
![eBUS binding configuration](doc/images/eBUS_binding_config.png?raw=true)

**Finally the things should show up in the Inbox:** 
![eBUS binding configuration](doc/images/eBUS_Binding_Inbox.png?raw=true)

## Alternatives to openHAB
* [FHEM (German)](https://wiki.fhem.de/wiki/EBUS) [Wikipedia [FHEM](https://de.wikipedia.org/wiki/FHEM) article (German)]
* [ioBroker Smarthome](https://www.iobroker.net/), [ioBroker.ebus](https://github.com/rg-engineering/ioBroker.ebus)
* [Home Assistant](https://www.home-assistant.io/integrations/ebusd/)

## References
* [openHAB](https://www.openhab.org/)
* [openHAB eBUS binding (outdated)](https://v2.openhab.org/addons/bindings/ebus1/)
* ["Unofficial" openHAB eBUS binding](https://github.com/csowada/openhab-ebus-binding)
* [Description of "unofficial" openHAB eBUS binding](https://github.com/csowada/openhab-ebus-binding/blob/main/bundles/org.openhab.binding.ebus/README.md)
* [eBUS daemon](https://github.com/john30/ebusd)
* [Firmware for ESP8266 and ESP32 allowing eBUS communication for ebusd](https://github.com/john30/ebusd-esp)
* [FHEM eBUS wiki article (German)](https://wiki.fhem.de/wiki/EBUS)
* [eBUS adapter which does not require trimming](https://ebus.github.io/adapter/base.en.html)
