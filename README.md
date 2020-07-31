# 3-Zone-5-Channel-Bus-Sensor-Hub

The 3 Zone - 5 Channel Bus Sensor Hub is a design recycled from an unimplmented project called Just Another Dust Collector Controller (https://github.com/jchambers2012/JADCC).  This project is currently being used to monitor sensors around my house as part of my home automation.  The PCB desing allows for 5 inputs and gobal input and outout over a single CAT5/6 cable.

## GPIO Layout

- "I" Only - Input Only
- "O" Only - Output Only 
- "IO"     - Can be used as both an Input or Output 
- "X"      - Special functions

###### ESP8266 Port Layout
- D0 - IO - IR via R3 resistor
- D1 - X  - SCL        - MCP23017, CHAIN-1, CHAIN-2 and LCD Header
- D2 - X  - SDA        - MCP23017, CHAIN-1, CHAIN-2 and LCD Header
- D3 - IO - Function B - Relay Header
- D4 - IO - Start      - Relay Header
- D5 - IO - Function A - Relay Header
- D6 - IO - Red LED    - Realy Header
- D7 - IO - Start LED  - Relay Header
- D8 - IO - Unused     - P5 Header
- A0 - IO - Unused     - P5 Header

###### mcp23017 Port Layout (numbering is in ESPHome)
- PGA 0-7:
-  0 - I  - Zone 1 - Sensor 1
-  1 - I  - Zone 1 - Sensor 2
-  2 - I  - Zone 1 - Sensor 3
-  3 - I  - Zone 1 - Sensor 4
-  4 - I  - Zone 1 - Sensor 5 
-  5 - I  - Zone 2 - Sensor 1
-  6 - I  - Zone 2 - Sensor 2
-  7 - I  - Zone 2 - Sensor 3
- PGB 0-7:
-  8 - I  - Zone 2 - Sensor 4
-  9 - I  - Zone 2 - Sensor 5
- 10 - I  - Zone 3 - Sensor 1
- 11 - I  - Zone 3 - Sensor 2
- 12 - I  - Zone 3 - Sensor 3
- 13 - I  - Zone 3 - Sensor 4
- 14 - I  - Zone 3 - Sensor 5
- 15 - I  - Gloabl Stop

###### Zone (1-3) RJ45
- Pin 1 - Zone X Sensor 5
- Pin 2 - Zone X Sensor 4
- Pin 3 - Zone X Sensor 3
- Pin 4 - Zone X Sensor 2
- Pin 5 - Zone X Sensor 1
- Pin 6 - Gobal "LED" to/from RELAY INTERCONNECT
- Pin 7 - Gobal "STOP" Input
- Pin 8 - Gobal 12v power rail


###### TO RELAY Header
- GND        - X - Common Power Ground
- Function B - IO - D3
- Function A - IO - D5
- Start LED  - IO - D7
- RED LED    - IO - D6
- 3v3        - x  - Common 3v from NodeMCU

###### RELAY INTERCONNECT Header
- RED LED - NA - Common return/send to all zoned for "LED" header
- STOP    - I  - Global Stop Input to MCP pin 15

###### FUNCTION Header
- IR+          - NA - IR via R3 resistor
- START BUTTON - IO - D7

###### CHAIN(1/2) Header (Ordered Label down)
- GND - X - Common Power Ground
- 3v3 - X - Common Power 3v from NodeMCU
- SCL - X - I2C Bus Clock
- SDA - X - I2C Bus Data
