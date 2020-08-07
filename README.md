# 3-Zone-5-Channel-Bus-Sensor-Hub

The 3 Zone - 5 Channel Bus Sensor Hub is a design recycled from an unimplmented project called Just Another Dust Collector Controller (https://github.com/jchambers2012/JADCC).  This project is currently being used to monitor sensors around my house as part of my home automation.  The PCB design allows for 5 inputs and global input and output over a single CAT5/6 cable.


###### RJ45 PCB Layout (Backside/Bottom):
 - See "Zone (1-3) RJ45" below for layout
 
![RJ45 PCB LAYOUT](https://github.com/jchambers2012/3-Zone-5-Channel-Bus-Sensor-Hub/blob/master/Images/RJ45_PINOUT.jpg)

 ###### Breakout Sensor Board One Global "Stop" and One Sensor (user select-able):
 - The RJ45s are wired in a way to all for multiple boards to be chained to allow for multiple "drops" withing the same zone using a common wire back to the hub.    
 - The "DOOR" IO is connected to 5 DIP switch.  Turning any of the switches to the ON/UP direction will connect one (or more) IO lines to the sensor(s) bus on the CAT5 bus.
 - The "STOP" IO is a global input that can be used for any function
 - The "LED" IO is a global return line that can optional be connected to a relay to allow for a global signal.  The LED is connected to the bus via the R2 resistor.  Can be bridged with a jumper wire if a LED resistor is not needed.  By default this bus line is not connected to anything on the hub but is exposed on the RELAY INTERCONNECT header and can be routed to a standalone optical optical coupler, to a relay or to be pulled low and use the 12v as a power bus.
 - The "12v" is directly connected to the 12v input from the power supply.  This could also be 5v by bridging/wiring 5v to both inputs.  The replaceable optical coupler has a built-in current limiting resistor so the bus can be directly shorted out to a IO line. 
 
![REMOTE ONE SENSOR PCB](https://github.com/jchambers2012/3-Zone-5-Channel-Bus-Sensor-Hub/blob/master/Images/REMOTE_1Z_1S.jpg)

###### Breakout Sensor Board One Global "Stop" and Five Sensor:
 - The RJ45s are wired in a way to all for multiple boards to be chained to allow for multiple "drops" withing the same zone using a common wire back to the hub.  
 - The "S1" to "S5" IO is connected directly to the sensor bus on the CAT5 bus.
 - The "STOP" IO is a global input that can be used for any function
 - The "LED" IO is a global return line that can optional be connected to a relay to allow for a global signal.  The LED is connected to the bus via the R2 resistor.  Can be bridged with a jumper wire if a LED resistor is not needed.  By default this bus line is not connected to anything on the hub but is exposed on the RELAY INTERCONNECT header and can be routed to a standalone optical optical coupler, to a relay or to be pulled low and use the 12v as a power bus.
 - The "12v" is directly connected to the 12v input from the power supply.  This could also be 5v by bridging/wiring 5v to both inputs.  The replaceable optical coupler has a built-in current limiting resistor and can be so the bus can be directly shorted out to a IO line. 
 
![REMOTE FIVE SENSOR PCB](https://github.com/jchambers2012/3-Zone-5-Channel-Bus-Sensor-Hub/blob/master/Images/REMOTE_1Z_5S.jpg)


###### HUB PCB v1.0.1: https://easyeda.com/jchambers2012/blower-sensing-controller_copy

![HUB PCB v1.0.1](https://github.com/jchambers2012/3-Zone-5-Channel-Bus-Sensor-Hub/blob/master/Images/PCB_HUB.jpg)

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
- Pin 1 - Zone X Sensor 5 (T568B Brown White)
- Pin 2 - Zone X Sensor 4 (T568B Brown)
- Pin 3 - Zone X Sensor 3 (T568B Blue White)
- Pin 4 - Zone X Sensor 2 (T568B Green)
- Pin 5 - Zone X Sensor 1 (T568B Green White)
- Pin 6 - Global "LED" to/from RELAY INTERCONNECT (T568B Blue)
- Pin 7 - Global "STOP" Input (T568B Orange White)
- Pin 8 - Global 12v power rail (T568B Orange)

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

###### FROM POWER SUPPLY Header
- 12v - X - 12v from power supply used for sensors.  Can be briged to 5v if long distance is not required.  There is no circuitry that steps down the 12 volts to the 5 volts power rails. A separate 5 volt power supply is needed.
- 5v  - X - 5v from power supply used for NodeMCU and (optional) LCD display
- GND - X - Common ground


### :warning: WARNING BEFORE PROCEEDING :warning: 
**YOU CAN BE ELECTROCUTED OR CAUSE BODILY HARM TO YOURSELF OR SOMEONE ELSE IF YOU DON'T KNOW WHAT YOU ARE DOING!**

**This project and I, the developer(s), do not take any responsibility for and we are not liable for any damage caused through use this system, be it indirect, special, incidental or consequential damages (including but not limited to damages for loss of business/home, loss of profits, interruption or the like, and/or loss of life).**

**All work produced by developers is provided “AS IS”. Developers make no warranties, expressed or implied, and hereby disclaims all implied warranties, including any warranty of merchantability and warranty of fitness for a particular purpose.  Developers are working as hobbyists.  It should never be assumed that they are trained or knowledgeable to give safety, electrical, or any other advice.**

Make sure you understand the risk of connecting a control system that can remotely control your blower system or other motors.  This system does not contain any hardware interlocks or watchdog system.  Make sure to contact an electrician when working with high or low voltage.  

**YOU ARE RESPONSIBLE** for your own safety and the proper operation of **YOUR** SYSTEM.  **YOU** are responsible to make sure the system is set up and meets any and all safety standards, electrical code and any and all codes of your local jurisdiction.

## Lack of Interlocking and Fail-Safe Operations
**The firmware and hardware does not contain any fail-safe systems or interlocks.**  It should never be used as part of a life safety system or control system where human lives depend on its safe or continual operation.  This control board should not be used as or in an emergency stop system.  Your system must contain its own emergency stop and isolation system to both safely power it off and perform maintenance.
