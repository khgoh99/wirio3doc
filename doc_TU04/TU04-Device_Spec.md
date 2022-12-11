
# Device Specification

Model Number: TU-04-C04

![](https://github.com/khgoh99/wirio3doc-iot-rfid-reader/raw/main/picture/Body%20View.png)

[Downlod Specification In PDF](TU-04-C04%20Product%20Specification.pdf)
# System Feature

## Wi-Fi/Ethernet Connected UHF RFID Tag Reader
- Connection is from device connected to server.
- Once system power up, it will auto create a persistence connection to the server without user intervention.
- Server can be placed either at public cloud, private cloud or LAN.
- Device able to work behind firewall.

## 4 Channel Long Range UHF Tag Reading

 - Based on Imping E710 chip with improved read rate and superior receive sensitivity for long rang reading.
 - Build in 1200 Tag Cache size for highspeed reading.
 - Able to match with various type of 50Ω Antenna to manage the tag detection range and angle.
 - Auto antenna detection and will only turn-on the antenna output channel if the antenna is detected.
 - User can also adjust the output power from 1dBm to 33dBm to manage the reading distance remotely though the server.
 - With the correct antenna and low lost feeder cable, the reading can achieve up to the reading range of 15meter.
 - Build in device core temperature sensor, providing remote temperature monitoring when the device is operating under high temperature environment.
 - Over temperature error auto stop and notification.
 - Build in Tag Selection Filter that only detect the tag that matches  or NOT matches the selection criteria.
 - Auto read tag data on any one of the tag’s memories banks when the  tag is detected.
 - Write/Lock/Kill Tag with Tag Selection Filter.

## Power of Ethernet support

- Support IEEE 802.3af and 802.3at.
- Input voltage ranging from 44V to 57V.
- In-rush current limit control.
- Over-temperature protection
- Support power supply at pin 1&2, 3&6 and 4&5, 7&8 on the RJ45 connector

## Internal power supply with DC/DC convertor to reduce power wastage

- Input DC 12V to 24V.
- Reverse polarity protection

## Onboard Input and Output Port

- 2 input port and 2 output port.
- Able to configure the input port as I/O input or user push button input.
- Push button input allow to auto user press action, single press, double press, triple press and long press (press and hold more than 4 second).
- Provide number of input on/off cycle counter to prevent missing cycle.
- Wet contact output design using MOSFET thus support up to 30V 1A output current without the wear and tear of the relay contact.
- Output port can be configured as standard High/Low output or Auto Pulsed output.
- Configurable pulse duration (configure separately for High level and Low-level period) and number of pulse cycle when trigger by server.

## Auto fetch real time clock from Internet Time Server.

- Auto connect with the Internet Time Server to fetch the Real time value (EPOC Time) when network is connected and internet link is available.
- Manually set time by server if internet link is not available.
- Auto readjust the time drift periodically.
- Append the EPOC time to all the message.

## Direct link with USB Connection

- Easily link up with the device without connecting to the network.
- Suitable for direct connection with PC/Host system locate beside the device.
- Just add an extra JSON layer of wrapper to wrap around the same JSON messaging standard used in the MQTT Broker Server communication.
- Thus provide an easy path for future system expansion, from localized system architecture to network-based system architecture.

## Network link with MQTT Broker Server

- Open Standard protocol and readily available either using paid version or free version of MQTT Broker Server.
- Messaging format based on JSON format.
- JSON messaging format is supported by various programming language and easily integrated to any existing system.

## Easy setup and configuration

- System configures with Android Apps.
- Provide detail device properties, e.g. model number, version number, etc.
- Connectivity selection either using Wi-Fi, Ethernet or USB Link.
- Upload WPA Enterprise Server private/public key.
- Server IP/Domain Name Setup.
- DHCP/Fix IP.
- Internet Time Server Setting.

## FW-Bus for I/O port expansion

- A short distance (Up to 10 meter) communication bus.
- Allow to attach external I/O Expansion Unit.
- Maximum up to 8 unit of I/O Expansion Unit, thus providing up to 64unit of input port and 64unit of output port.

# Hardware Specification
## Power and Enclosure Specification
|Item|Description|
|--|--|
|Input Voltage|DC 12V to 24V or POE  |
|Supported POE|IEEE802.af/at, RJ45 Connector Power pin on 1&2, 3&6 and 4&5, 7&8.|
| System Power Consumption | 15W Max |
|Operation Humidity|20%-90%RH|
|Operation Temperature|25°C to 45°C|
|Storage Humidity|10-95RH|
|Storage Temperature|0°C to 85°C|
|Enclosure Dimension |131mm (W) x 130mm (L) x 28mm (H) with 4x mounting screw hole|
|Enclosure Type|Aluminum Extrusions|

## RFID Reader Specification
|Item|Description|
|--|--|
|Antenna Channel|	4 Channel|
|Operation Frequency|	919MHz~923MHz Auto Hopping (According to MCMC Class Assignment for RFID)|
|Output Power|	33dBm Max, User Adjustable in 1dBm Step|
|UHF Tag Protocol|	EPC global UHF Class 1 Gen 2 ISO 18000-6C|

## Wi-Fi Specification
|Item|Description|
|--|--|
|Frequency|	2.4Ghz~2.5Ghz
|Supported Wi-Fi Protocol|	802.11 b/g/n|
|Antenna Type|	External|
|Security Protocol|	WPA/WPA2 personal, WPA/WPA2 Enterprise|
|Encryption Protocol|	WEP/TKIP/AES|


## Ethernet Specification
|Item|Description|
|--|--|
|Speed|	RJ45, 10/100 Mbps|
|Power over Ethernet|	IEEE802.af/at, RJ45 Connector Power pin on 1&2, 3&6 and 4&5, 7&8.|
|Voltage|	44V~57V DC|

## USB Type-C Port Specification
|Item|Description|
|--|--|
|Supported Protocol|	USB Virtual Comm Port
|Baud|	921600 Baud, 8bit, no-parity, 1 stop bit

## Backend Server Connectivity
|Item|Description|
|--|--|
|Server Connection|	MQTT Broker with TCP, TCP-TLS, Web-Socket Connection|
|Server Port|	User Definable|
|Encryption/Security|	Public CA, Self-Signed Certificate|
|Messaging Format|	JSON|
|Other|	NTP auto RTC update|

## Output Port Specification
|Item|Description|
|--|--|
|Total Output Port Channel|	2 Channel|
|Connection Type|	N Type Sink to Ground when on|
|Max V+ Voltage|	30V|
|Max Sink Current|	1A (Non-Inductive Load)|

![Output Port Architecture](https://github.com/khgoh99/wirio3doc-iot-rfid-reader/raw/main/picture/io%20port%20design-Output%20Port.png)

## Input Port Specification
|Item|Description|
|--|--|
|Input Port|2 Channel|
|Connection Type|N Type, External Sink to Ground to Trigger On|
|Max Sink Current|5mA|

![Input Port Architechture](https://github.com/khgoh99/wirio3doc-iot-rfid-reader/raw/main/picture/io%20port%20design-Input%20Port.png)

## FWBus Specification
|Item|Description|
|--|--|
|Port|Pin A+GND, Pin B+GND|
|Connection Type|Open Collector|
|Max Sink Current|30mA Max|
|Max Cable Length|Up to 10 Meter with Cat5e Cable|


