# Industrial IoT Remote I/O

Model Number: RP2-1204M

12 Bidirectional Opto-isolated input channel, 4 Relay Contact Output Channel equiped with Modbus slave interface.

Enclusure is Water/Dust resistance. Please take note that to prevent the water/dust to leak into the enclosure, please make sure that the wire going through the wire gland is having outter dimeter between 6.5mm to 11mm (PG13.5) and 4mm to 8mm(PG9).

[Downlod Hardware Specification In PDF](pdf/RP2-1204M%20Product%20Specification%20Rev.1.pdf)

[Download Modbus Address Defination](pdf/RM1204M%20Modbus%20Address.pdf)

[Download MQTT Communication Base Specification](pdf/WiRIO3%20MQTT%20Base%20Communication%20Spec%20Rev%207.pdf)

[Download MQTT Communication Speciation for RP2-1204M](pdf/WiRIO3%20RP2-1204M%20WAN-IO%20Communication%20spec%20Rev%203.pdf)

# System Feature

- Connection is from device connected to server.
- Once system power up, it will auto create a persistence connection to the server without user intervention.
- Server can be placed either at public cloud, private cloud or LAN.
- Device able to work behind firewall.
- Modbus Slave Interface support multiple range of Baudrate.

## Network link with MQTT Broker Server

- Open Standard protocol and readily available either using paid version or free version of  MQTT Broker.
- Messaging format based on JSON format.
- JSON messaging format is supported by various programming language and easily integrated to any existing system.
- Device support Secure WebSocket or Secure TCP connection to MQTT Broker.

## Auto fetch real time clock from Internet Time Server.

- Auto connect with the Internet Time Server to fetch the Real time value (EPOC Time) when network is connected and internet link is available.
- Manually set time by server if internet link is not available.
- Auto readjust the time drift periodically.
- Append the EPOC time to all the message.

## Easy setup and configuration

- System configures with Android Apps.
- Provide detail device properties, E.g., model number, version number, etc.
- Connectivity selection either using Wi-Fi and/or Modbus RTU Slave.
- MQTT Server IP/Domain Name Setup.
- DHCP/Fix IP.
- Internet Time Server Setting.

## Other

- Water/Dust resistance enclosure.
- Support wide supply input voltage, 12V DC to 24V DC.
- All terminal block connector is detachable for easy installation.
- External water/dust resistance link indicator and configuration push button.
- External configuration push button can be disabled.

# Hardware Specification
## Power and Enclosure Specification

|Item|Description|
|--|--|
|Input Voltage|DC 12V to 24V  |
|System Power Consumption | 5W Max |
|Operation Humidity|20%-95%RH|
|Operation Temperature|25°C to 55°C|
|Storage Humidity|10-95%RH|
|Storage Temperature|0°C to 85°C|
|Enclosure Dimension |68mm (W) x 99.5mm (L) x 50mm (H) (Exclude Wire Glands Outlet)|
|Enclosure Type|Water/Dust resistance Durable Industrial PPM Casing|

## Input Channel

|Item|Description|
|--|--|
|Total Channel|12|
|Input Type|Bi-directional Opto-Isolated, User can define either common positive or common negative|
|Arrangement|4 Channel per Group, total 3 groups. Each group will have individual common input|
|Input Range|12V to 24V DC|

## Output Channel

|Item|Description|
|--|--|
|Total Channel|4|
|Output Type|Relay dry contact|
|Arrangement|One common output for all 4-output channel|
|Current Rating|Each channel 5A Max. Total channel 5A Max.|

## Wi-Fi Specification

|Item|Description|
|--|--|
|Frequency|	2.4Ghz~2.5Ghz
|Supported Wi-Fi Protocol|	802.11 b/g/n|
|Antenna Type|	Internal|
|Security Protocol|	WPA/WPA2 personal, WPA/WPA2 Enterprise|
|Encryption Protocol|	WEP/TKIP/AES|

## Modbus Inteface

|Item|Description|
|--|--|
|Protocol|	Modbus RTC Slave |
|Baud Rate|	4800 Baud to 115200 Baud, 8-N-1|
|Slave Address|	1 to 247|

## Backend Server Connectivity

|Item|Description|
|--|--|
|Server Connection|	MQTT Broker with TCP, TCP-TLS, Web-Socket, SSL Web-Socket Connection|
|Server Port|User Definable|
|Encryption/Security|Public CA|
|Messaging Format|JSON|
|Other|NTP auto RTC update|

## Device Outer Dimension

![Dimension](picture/RP2-1204M%20outer%20dimension.png)