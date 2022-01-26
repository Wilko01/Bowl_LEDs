# Bowl with LEDS
Control the intensity of the LEDS via a NODEMCU with PWM and add it to Home Assistant

## Description and operation instructions
..

 ## Technical description
.

### Parts
1 x NodeMCU

<img src="Images/ESP8266_NodeMCU.jpg" alt="drawing" width="500"/>



1 x 10k resistor as pull down resistor


### Schematic overview
<img src="Images/Schematic_overview.jpg" alt="drawing" width="500"/>
 
•	Connect the 230V side of the relay according to the installation instructions of the boilerNodeMCU with. See the relay socker pinout below on how to connect.

•	Connect the relay contact to the 3,3V of the NodeMCU and the other side to D6.

•	Connect the 10k resistor to D6 and to GND to use it as a pull down resistor.

### ESPHome installation
See the instructions https://github.com/Wilko01/ESPHome  (not listed here)


### ESPHome Configuration in Home Assistant
Create a new device  with this code:
```
#Running via ESPHOME

#Runs on a NodeMCU

esphome:
  name: bowl-leds

esp8266:
  board: nodemcuv2

# Enable logging
logger:

# Enable Home Assistant API
api:

ota:
  password: "1e7c9c2b1830d88364f40572c813b20f"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Bowl-Leds Fallback Hotspot"
    password: "7lgvJ8aOzZ3w"

captive_portal:

#begin code

output:
  - platform: esp8266_pwm
    pin: D4
    frequency: 1000 Hz
    id: pwm_output


fan:
  - platform: speed
    output: pwm_output
    name: "Bowl-LEDs"
#end code
```

### Interface
#### Home Assistant
Home Assistant is connected via the ESPHome integration.

##### card
Create a card in the dashboard of Home Assistant with this code
```
type: entities
entities:
  - fan.bowl_leds
```


### Testing
Turn the led on and off via the card at the dashboard

### Information
- [PNP amplifier circuit](https://circuitdigest.com/electronic-circuits/transistor-as-an-amplifier-circuit)
- [ESPHOME PWM control](https://esphome.io/components/fan/speed.html)

Generic
- [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)


### Problems
..

### Wishlist
..


