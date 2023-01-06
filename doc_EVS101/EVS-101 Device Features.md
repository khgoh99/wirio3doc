
# Industrial IoT Enviroment Sensor

Model Number: EVS-101

Temperature, Humidity and Room Pressure Sensor Logger

![](doc_EVS101/picture/evs-101%20device.png)

[Downlod Specification In PDF](pdf/EVS-101%20Product%20Specification%20Rev.1.pdf)
# System Feature

## Wi-Fi/Ethernet Connected UHF RFID Tag Reader

- Connection is from device connected to server.
- Once system power up, it will auto create a persistence connection to the server without user intervention.
- Server can be placed either at public cloud, private cloud or LAN.
- Device able to work behind firewall.

## Network link with MQTT Broker Server

- Open Standard protocol and readily available either using paid version or free version of  MQTT Broker.
- Messaging format based on JSON format.
- JSON messaging format is supported by various programming language and easily integrated to any existing system.
- Device support Secure WebSocket or Secure TCP connection to MQTT Broker.

## Direct link with USB Connection

- The device also can be configured to use USB Connection without connecting to the network.
- Suitable for direct connection with PC/Host system locate beside the device.
- Just add an extra JSON layer of wrapper to wrap around the same JSON messaging standard used in the MQTT Broker Server communication.
- Thus provide an easy path for future system expansion, from localized system architecture to network-based system architecture.

## Device’s sensors with MEMS

- Build in with Micro-electromechanical systems sensors (MEMS) technology
- Highly accurate and fully digital output direct from the sensors.
- Sensors are calibrated and accuracy are guarantee by sensor manufacturer.

## TFT display

- Colorful TFT display design
- Eye-caching of the sensor reading from a far.

## Auto fetch real time clock from Internet Time Server.

- Auto connect with the Internet Time Server to fetch the Real time value (EPOC Time) when network is connected and internet link is available.
- Manually set time by server if internet link is not available.
- Auto readjust the time drift periodically.
- Append the EPOC time to all the message.

## Easy setup and configuration

- System configures with Android Apps.
- Provide detail device properties, E.g., model number, version number, etc.
- Connectivity selection either using Wi-Fi, Ethernet or USB Link.
- Upload WPA Enterprise Server private/public key.
- Server IP/Domain Name Setup.
- DHCP/Fix IP.
- Internet Time Server Setting.

# Hardware Specification
## Power and Enclosure Specification

|Item|Description|
|--|--|
|Input Voltage|DC 5V USB-C Connector  |
|System Power Consumption | 15W Max |
|Operation Humidity|20%-95%RH|
|Operation Temperature|25°C to 45°C|
|Storage Humidity|10-95%RH|
|Storage Temperature|0°C to 85°C|
|Enclosure Dimension |59mm (W) x 88mm (L) x 37mm (H) (Exclude sensor wire and mounting hook, 109mm(L) with mounting hook)|
|Enclosure Type|ABS and Acrylic|

## Sensors Specification

|Item|Description|
|--|--|
|Temperature and Humidity Sensor|Model SHT-40 By Sensirion|
|Temperature Accuracy|Up to ±0.1°C|
|Relative Humidity Accuracy|Up to ±1.5%RH|
|Temp/Humidity Operating Range|0~100%RH, -40~125°C|
|Pressure Sensor|Model BMP280 By Bosch Sensortech|
|Pressure Absolute Accuracy|±1mBar @950mBar~1050mBar, 0°C ~40°C|
|Pressure Operating Range|300mBar~1100mBar|

## Wi-Fi Specification

|Item|Description|
|--|--|
|Frequency|	2.4Ghz~2.5Ghz
|Supported Wi-Fi Protocol|	802.11 b/g/n|
|Antenna Type|	Internal|
|Security Protocol|	WPA/WPA2 personal, WPA/WPA2 Enterprise|
|Encryption Protocol|	WEP/TKIP/AES|


## Ethernet Specification

|Item|Description|
|--|--|
|Speed|	RJ45, 10/100 Mbps|

## USB Type-C Port Specification

|Item|Description|
|--|--|
|Supported Protocol|USB Virtual Comm Port|
|Baudrate|115200 Baud, 8bit, no-parity, 1 stop bit|

## Backend Server Connectivity

|Item|Description|
|--|--|
|Server Connection|	MQTT Broker with TCP, TCP-TLS, Web-Socket Connection|
|Server Port|User Definable|
|Encryption/Security|Public CA, Self-Signed Certificate|
|Messaging Format|JSON|
|Other|NTP auto RTC update|

## Device Outer Dimension

![Dimension](picture/evs-101%20dimension.png)

## Mem Sensor Datasheet

[Sensirion web page for the Temperature/Humdity Sensor SHT40](https://sensirion.com/products/catalog/SHT40/)

[Temperature/Humdity Sensor Datasheet in pdf](pdf/Sensirion_Datasheet_SHT4x.pdf)

[Bosch Sensortech web page for Room Pressure Sensor BMP280](https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/bmp280/)

[Room Pressure Sensor Datasheet in pdf](pdf/bst-bmp280-ds001.pdf)

