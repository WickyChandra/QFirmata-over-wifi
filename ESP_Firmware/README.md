Wiring
===
The Arduino and ESP will communicate through serial, the wiring between ESP and Arduino should be like this:
1. 3.3V ESP to 3.3V Arduino  or 5V ESP to 5V Arduino (depend on ESP module type)
2. GND  ESP to GND  Arduino
3. Tx   ESP to Rx   Arduino
4. Rx   ESP to Tx   Arduino

*I recommend to put the power source on Arduino side to make sure other module connected to arduino get enough power.
---
Usage
---
This is one of the methedes for the PC to communicate with the Arduino that connected to ESP:
1. You can use [virtual serial port](<https://www.hw-group.com/software/hw-vsp3-virtual-serial-port>) 
2. Install the single version (recommended)
3. Navigate to Virtual Serial Port tab
4. Click login and it will automaticly input the pass
5. Just input your ESP8266 IP address to the app and select the serial port number (COMxx).
6. Click create COM and wait the LAN status connected
---
How to Flash
===
Via Arduino IDE (work for both ESP8266 and ESP32)
---
The sketch used in this methode based on [this project](<https://www.hackster.io/techbase_group/arduino-esp32-serial-port-to-tcp-converter-via-wifi-66d341>).
1. Choose Arduino sketch that suits your devices
2. open the .ino file
3. make sure you have ESP32 or ESP8266 board manager installed, check this if not installed for [ESP8266](<https://arduino-esp8266.readthedocs.io/en/latest/installing.html>) or [ESP32](<https://www.hackster.io/abdularbi17/how-to-install-esp32-board-in-arduino-ide-1cd571>)
4. setup ssid and password of your network in //wifi config section
5. in //ethernet setup section, configure your ip address setup to fit your network configuration to make ESP has static IP and set it as your TCP server adddress, if your network not allowing static IP request, just command this section to make it recive dynamic IP.
7. in //rs-server config section, configure your tcp server port
8. in // rs port config section, configure your serial connection
9. if you're using dynamic IP address (DHCP), check the serial monitor to get your board IP address info from the debug messages.
---

Via NodeMCU-PyFlasher(only for esp8266 using ESP-Link firmware)
---
1. open NodeMCU-PyFlasher-with-ResetLocale.exe
2. in NodeMCU Firmware section choose the target.bin file in this folder
3. select Baud rate at "115200", Flash mode at "DIO", erase flash at "no"
4. connect your NodeMCU to computer, then select your NodeMCU serial port
5. Flash NodeMCU and wait until it finished

How to setup
1. Once the NodeMCU boot into ESP-Link firmware it will act as access point, find the access point named ESP-(last 4 character of your MAC address) and conect
2. Open the ESP-Link default web server at 192.168.4.1
3. Go to WiFi Station Configuration and Switch to STA+AP mode
4. Connect to your WiFi network and wait until getting an IP address
5. I prefer to use static IP instead DHCP for easier connection
6. Reconnect to your Wifi network and go to IP address of your ESP-link and it will show you the web server
7. Go to Microcontroller Console, make sure the fmt on 8N1 and select the baud rate that match your arduino and firmata baud rate
