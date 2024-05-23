*TU-04-C04 Multi-Channel RFID Reader Communication Specification Rev 4*










![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.001.png)![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.002.png)![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.003.png)![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.004.png)

<a name="_toc83063359"></a>
# Contents
[Overview	3](#_toc138179066)

[MQTT Communication	3](#_toc138179067)

[Device and Peripheral	3](#_toc138179068)

[Type of Attribute	4](#_toc138179069)

[Device Only Attribute	4](#_toc138179070)

[Share Attribute	4](#_toc138179071)

[Communication with the device through MQTT Broker	4](#_toc138179072)

[MQTT Server Setup	5](#_toc138179073)

[MQTT Topic	5](#_toc138179074)

[Overview on function of each topic	6](#_toc138179075)

[Device Publish System Attribute	6](#_toc138179076)

[Device Update System Attribute	6](#_toc138179077)

[Telematics Data	6](#_toc138179078)

[RPC Request	6](#_toc138179079)

[RPC Reply	6](#_toc138179080)

[Communication Spam Protection	6](#_toc138179081)

[JSON Messages on Each Topic	7](#_toc138179082)

[Device Publish System Attribute	8](#_toc138179083)

[Example of the system attribute data packet for the peripheral .	9](#_toc138179084)

[Last Will Message on Device Publish System Attribute Topic	9](#_toc138179085)

[Update Device’s System Attribute	10](#_toc138179086)

[Telematics Data	11](#_toc138179087)

[RPC Request and RPC Reply	12](#_toc138179088)

[Communicate Through USB Serial Port	14](#_toc138179089)

[Serial Port Setting	14](#_toc138179090)

[MQTT Topic Conversion	14](#_toc138179091)

[Other Differences on MQTT Topic	17](#_toc138179092)

[The Device Peripheral – Core System	18](#_toc138179093)

[System Peripheral	18](#_toc138179094)

[System Only Attribute	18](#_toc138179095)

[Share Attribute	19](#_toc138179096)

[RPC Call and Response	19](#_toc138179097)

[Limitation and Counter Measure of MQTT server	20](#_toc138179098)

[The Device Peripheral – RFID Reader	21](#_toc138179099)

[RFID Reader Peripheral	21](#_toc138179100)

[Attribute	21](#_toc138179101)

[Telematics Data	28](#_toc138179102)

[RPC Call and Response	30](#_toc138179103)

[RFID Tag Memory Map Layout	38](#_toc138179104)

[Tag Selection/Singulation	39](#_toc138179105)

[Example	39](#_toc138179106)

[Tag Locking and Tag Password	40](#_toc138179107)

[Gen2 Tag Passwords	40](#_toc138179108)

[Lock Mask and Lock Action	40](#_toc138179109)

[Tag Locking State Chart	41](#_toc138179110)

[Tag Locking process	41](#_toc138179111)

[Tag Reading Process	42](#_toc138179112)

[TAG Reading/Writing Return Code	43](#_toc138179113)

[The Device Peripheral – Output Port	44](#_toc138179114)

[Output Port Peripheral	44](#_toc138179115)

[Attribute	44](#_toc138179116)

[Telematics Data	45](#_toc138179117)

[RPC Call and Response	45](#_toc138179118)

[The Device Peripheral – Input Port	47](#_toc138179119)

[Input Port Peripheral	47](#_toc138179120)

[Attribute	47](#_toc138179121)

[Telematics Data	48](#_toc138179122)

[RPC Call and Response	48](#_toc138179123)




# <a name="_toc138179066"></a>Overview
## <a name="_toc138179067"></a>MQTT Communication
The device will communication with the backend host server though a MQTT Broker. For more information on the MQTT Broker working concept, please refer to the link below,

`	`<https://www.hivemq.com/mqtt-essentials/>

<https://www.youtube.com/watch?v=z4r4hIZcp40>

## <a name="_toc83063360"></a><a name="_toc138179068"></a>Device and Peripheral
Each WiRIO3 Device can contain multiple type of Peripheral, e.g., Input Port, Output Port, Environment Sensor, etc.  The host can request for the device properties which also include the Peripheral availability in the device any time by sending a blank JSON packet “ {} “ to the device.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.005.png)Each Peripheral will have a Peripheral “cmdkey” included as part of the JSON key. This JSON key will be used as the reference name that allow the Host Server to direct send and received RPC or Telematics info to/from the peripheral.


<a name="_toc83063361"></a>
## <a name="_toc138179069"></a>Type of Attribute
Attribute in the device will include any system properties and peripheral configuration setting in the device. The Attribute is divided in to 2 type/category.

- Device Only Attribute
- Share Attribute
### <a name="_toc83063362"></a><a name="_toc138179070"></a>Device Only Attribute
This type of attribute is only allowing the device to modify and update to the Host Server. Host Server **do not** allow to modify the value of the attribute.

The device will publish any changes on attribute in the Device Publish System Attribute topic.
### <a name="_toc83063363"></a><a name="_toc138179071"></a>Share Attribute
Both the device and the host are allowed to modify the attribute value.
## <a name="_toc83063364"></a><a name="_toc138179072"></a>Communication with the device through MQTT Broker
The WiRIO3 Device and Host Server (backend Management Server) will connect to a MQTT Broker. The device will subscribe to the require topic to listen to any massage published by the Host Server and publish any sensor Telematics information in to the pre-defined MQTT topic.

The Host Server require to subscribe to the device publish topic to listen to the device’s published message and process the sensor data accordingly.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.006.png)


# <a name="_toc83063365"></a><a name="_toc138179073"></a>MQTT Server Setup

|MQTT Broker Connection Type|MQTT TCP/Web-Sock connection with JSON as data packet format|
| :- | :- |
|TCP Port Number|User configurable|
|Encryption|Public CA or Private Certificate, TLS/SSL|

\*\* The server address and port number can be change according to the user requirement using the WiRIO3 Device Configuration Android Apps.

The supported MQTT Topic format are,

- WiRIO3 Topic Format
- Thingsboard.io Topic Format
- User Customizable Topic Format

The selection and configuration of the MQTT Topic can be done by using the WiRIO3 Device Configuration Android Apps.
# <a name="_toc83063366"></a><a name="_toc138179074"></a>MQTT Topic 
In each of the MQTT Topic format selected, there is total of 5 MQTT Topic either for device to publish messages to the server or for device to subscribe the topic in order to listen to any messages from the server.

The 5 MQTT Topic required by the device are as follow,

|*Type of Topic*|*Device*|*Host Server* |
| -: | :- | :- |
|*Telematics Data*|Publish|Subscribe|
|*Device Publish System Attribute*|Publish|Subscribe|
|*Update Device’s System Attribute*|Subscribe|Publish|
|*RPC Request*|Subscribe|Publish|
|*RPC Reply*|Publish|Subscribe|

The default topic setting is as below,

|*Type of Topic*|*WiRIO3 Default*|*Thingsboard.io Default*|
| -: | :- | :- |
|*Telematics Data*|W3/<DeviceID>/telemetry|v1/devices/me/telemetry|
|*Device Publish System Attribute*|W3/<DeviceID>/attributes|v1/devices/me/attributes|
|*Update Device’s System Attribute*|W3/<DeviceID>/attributes|v1/devices/me/attributes|
|*RPC Request*|W3/<DeviceID>/rpc/request/+|v1/devices/me/rpc/request/+|
|*RPC Reply*|W3/<DeviceID>/rpc/response/+|v1/devices/me/rpc/response/+|

The <DeviceID> is the unique ID of the device in the format of WIRIO3\_AABBCCDDEEFF where AABBCCDDEEFF is the 6 bytes hex string in upper case. E.g. WIRIO3\_43DF01543AF0.

The “+” wildcard on the RPC request and RPC reply topic will allow the subscriber to receive any topic with other info attached at the end of the topic. For more detail on the MQTT topic wildcard, please refer to the Standard MQTT Broker documentation.
# <a name="_toc83063367"></a><a name="_toc138179075"></a>Overview on function of each topic
## <a name="_toc83063368"></a><a name="_toc138179076"></a>Device Publish System Attribute
The device will publish any system and peripheral attribute setting in this topic. During initial connection to the MQTT Broker, the device will auto publish the all the system and peripheral attributes through this topic. 
## <a name="_toc83063369"></a><a name="_toc138179077"></a>Device Update System Attribute
The device will subscribe to this topic and monitor for any request from the Host Server to update the **share** attributes. If the Host Server require to modify the Share Attribute, the Host Server will publish the request into this topic.
## <a name="_toc83063370"></a><a name="_toc138179078"></a>Telematics Data
The device will use this topic to push the device’s telematics data. The Host Server should monitor this topic for any new sensor information update from the device and process the sensor data accordingly.  
## <a name="_toc83063371"></a><a name="_toc138179079"></a>RPC Request
If the server requires the device to do certain action, the Host Server will publish the request into this topic. On the request message’s topic, Host Server is required to publish the message into the topic with a <RequestID> append at the end of the topic, e.g. W3/<DeviceID>/request/<RequestID>. During the RPC reply, the <RequestID> will be append at the end of the reply message’s topic. The device **will not** do any validation/checking on the <RequestID> value.

Please note that the <RequestID> is compulsory. The system can provide any arbitrary number when publishing the RPC Request.

E.g. 

W3/C45BBE821F38/request/48
## <a name="_toc83063372"></a><a name="_toc138179080"></a>RPC Reply
Once the device received and processed the RPC request from the server, the device will reply to the server through this topic. The <RequestID> on the request message’s topic, will be append to the reply message’s topic.
## <a name="_toc138179081"></a>Communication Spam Protection
On all the device listening topic (Device Update System Attribute Topic and RPC Request Topic), in combine, the timing between each message must have a minimum gap period of 150ms. Any data packet that has timing gap period that less than this, will be ignore.


# <a name="_toc83063373"></a><a name="_toc138179082"></a>JSON Messages on Each Topic
On the **all the packet sending out from the device**, it will have minimum number of keys as below,

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.007.png)

On **all the packet sending to the device** from the back-end server, the minimum number of keys require are the “deviceid” key,

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.008.png)

If the “deviceid” do not match the ID of the device, the message will be ignored.

But if the MQTT Topic format selection is either WiRIO3 format or Thingsboard.io format, the key “deviceid” is **NOT** required and will be ignore by the device.

Others JSON key that the device published out are as below,

|***Key***|**Description**|
| -: | :- |
|*deviceid*|The unique identifier for each device|
|*sec*|\*\* Current Epoch times in second. (Only available in Telematics Topic)|
|*rssi*|Device Wi-Fi Received Signal Strength Index (Only Available if device is on Wi-Fi Link) |
|*pktno*|A running number increase by 1 when device **publish** a packet on any of the device publish topic|

\*\* The EPOCH time “sec”, only available (in Telematics Topic) if the device is able to obtain the real time clock through the NTP server or Host Server has Updated the “s.sys.epochsec” key and “d.sys.epochvalid” is True. 

The detail NTP server setting and configuration is available in the WiRIO3 Device Configuration Android Apps.

<a name="_toc83063374"></a><a name="_toc83063376"></a>
## <a name="_toc138179083"></a>Device Publish System Attribute
During the device initial connection, it will publish out the all the available system and peripheral attribute. 

The property key listed above starting with “d.xxx.xxx” is Device Only Attribute and not modifiable by the Host Server. If there are any changes on the system attribute, the device will publish it again.

The property key with “s.xxx.xxx” is Share Attribute that can be modify by either device or Host Server (Refer to section “Device Update System Attribute Topic” for further information). 

If the device is having any device peripheral configurable value, the system will publish it together with above attribute.  Below is the example of the Device Published Attribute.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.009.png)

<a name="_toc83063375"></a>
### <a name="_toc138179084"></a>Example of the system attribute data packet for the peripheral .

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.010.png)

Example of a device d.sys.perip attribute indicating that the device is having more than one Peripheral.
### <a name="_toc138179085"></a>Last Will Message on Device Publish System Attribute Topic
During device initial connection to the MQTT Broker, it will register a Last Will message that will allow the MQTT Broker to publish out when the device is disconnected. The JSON message for the Last Will Message is as below,

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.011.png)

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.012.png)

### <a name="_toc83063377"></a><a name="_toc138179086"></a>Update Device’s System Attribute
If there is any value that allow the Host Server to modify including the device peripheral setting, the Host Server can publish the key require to modify it in this topic. 

E.g., Change the UHF reader transmission power.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.013.png)

Example of the device response.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.014.png)

If the Host Server send a blank JSON with only the “deviceid” key (for customized MQTT Topic), or total blank JSON packet (for WiRIO3 and Thingsboard Topic) the device will publish out all the device available attribute in the Device Publish System Attribute Topic.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.015.png)

E.g. Blank request by the host for user customize MQTT Topic. 

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.016.png)

E.g., Blank request by the host for WiRIO3 or Thingsboard.io MQTT Topic.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.017.png)


## <a name="_toc83063378"></a><a name="_toc138179087"></a>Telematics Data
The device will use this topic to publish any telematics data detected by the host. On the detail key/value on the telematics data, please refer to the individual device communication specification for more information.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.018.png)

E.g., Above is a Temperature/Humidity Sensor device publish out the latest temperature and humidity reading.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.019.png)


## <a name="_toc83063379"></a><a name="_toc138179088"></a>RPC Request and RPC Reply
![C:\Users\khgoh\AppData\Local\Microsoft\Windows\INetCache\Content.Word\Wirio3 rpc process.png](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.020.png)The Host Server can request for action on the device’s peripheral that has RPC feature. E.g. Output Port Peripheral.

The host request to set the output port on channel 0 and channel 2 in RPC request topic, 

e.g. 

W3/ WIRIO3\_43DF01547AB1/rpc/request/33 

or 

`	`W3/ WIRIO3\_43DF01547AB1/rpc/request/  (if the <RequestID> is not required).

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.021.png)

Once the device has processed the RPC request, it will reply the request in the RPC Response topic, e.g. 

W3/ WIRIO3\_43DF01547AB1/rpc/response/33

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.022.png)

If the RCP request is successfully processed, it will return the key/value,

“r.<cmdkey>.result” : true

Else it will return false. 

“r.<cmdkey>.result” : false

In example above, the <cmdkey> is “outputport”.

Please take note that the RPC request is a **blocking process**. The device will only handle the subsequence request after the RPC Reply is published out. Any request received before the device publish the reply message will be directly return with false result.


# <a name="_toc138179089"></a>Communicate Through USB Serial Port
For the hardware that support serial port communication, user has the option to communication with the device through USB serial port while maintaining the JSON communication format structure.

User can use either Serial Port **OR** MQTT Broker as the JSON communication transport device. Selection can be done using the WiRIO3 Device Configuration Android Apps.

User can only select either using the MQTT Broker **OR** using Serial Port (USB Virtual Comm. Port) for communication. The MQTT Broker will take precedent and disable the Serial Port Communication during device boot up if both of the interface is enabled.
## <a name="_toc138179090"></a>Serial Port Setting

|*Item*|*Setting*|
| -: | :- |
|*Baud Rate*|921600|
|*Bit Number*|8|
|*Number of Parity Bit*|None|
|*Number of Stop Bit*|1|

## <a name="_toc138179091"></a>MQTT Topic Conversion
Due to serial communication only has one communication channel, all the topic involved in the MQTT Communication will be converted into JSON object key in the JSON communication packet. The original JSON message will be encapsulated under the topic converted JSON key bracket. List of the MQTT topic conversion is as below,

|*MQTT Topic*|*Convert to JSON Key*|*Direction*|
| -: | :- | :- |
|*Telematics Data*|telematics|From Device|
|*Device Publish System Attribute*|attribute|From Device|
|*Update Device’s System Attribute*|attribute|From Host/Server|
|*RPC Request*|rpcreq|From Host/Server|
|*RPC Reply*|rpcreply|From Device|

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.023.png)![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.024.png) Example of the RPC Request and RPC Reply,



Example of the telematics packet received from the device are as below,

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.025.png)




Example of Attribute request,

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.026.png) 

And the Attribute reply.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.027.png)


## <a name="_toc138179092"></a>Other Differences on MQTT Topic
The other difference between the MQTT Broker vs serial port communication beside the MQTT Topic, is as below,

- <RequestID> are not supported in Serial Communication
- JSON key “rssi” is not available in Serial Communication
- Attribute related with MQTT server or Wi-Fi/Ethernet interface is not relevant, please ignore it.
- JSON key “d.sys.linkup” will always “true”.


# <a name="_toc138179093"></a>The Device Peripheral – Core System
## <a name="_toc138179094"></a>System Peripheral

|***Key***|**Value**|
| -: | :- |
|*keycmd*|sys|
### <a name="_toc138179095"></a>System Only Attribute

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*d.sys.model*|String|<p>Device Model (TU-04-C04)</p><p></p>|
|*d.sys.name*|String|<p>Device Name (WiRIO3 IoT Reader)</p><p></p>|
|*d.sys.desc*|String|<p>Device Description (IoT 4ch UHF RFID Tag Reader)</p><p></p>|
|*d.sys.fwid*|String|<p>Firmware ID (E.g., 0507-04-EM109R1)</p><p></p>|

|***Key***|**Description**|
| -: | :- |
|*d.sys.addr*|<p>Device current IP address</p><p></p>|
|*d.sys.iface*|<p>Device connected interface, either “WiFISTA” for Wi-Fi Link Interface or “ETHERNET” for Ethernet Link Interface</p><p></p>|
|*d.sys.ssid*|<p>Device Wi-Fi Received Signal Strength Index (Only Available if device is on Wi-Fi Link)</p><p></p>|
|*d.sys.fwid*|<p>Device Firmware ID (unique for each type of device)</p><p></p>|
|*d.sys.datecode*|<p>Firmware version Date Code in YYMMDD</p><p></p>|
|*d.sys.model*|<p>Device model number</p><p></p>|
|*d.sys.name*|<p>Device Name</p><p></p>|
|*d.sys.desc*|<p>Device description</p><p></p>|
|*d.sys.perip*|<p>Available device peripheral in JSON Array. Data in this key will provide detail properties of the available peripheral in the device. Available key under d.sys.perip are as below,</p><p>cmdkey : The peripheral  reference ID.</p><p>feature : Value that describing the feature of this peripheral. </p><p></p>|
|*d.sys.linkup*|<p>True of False to indicate if the device is connected or not connected to the MQTT Broker server.</p><p></p>|
|*d.sys.epochvalid*|<p>True or false to indicate if the EPOCH time is valid or not valid</p><p></p>|
|*d.sys.rpcbusy*|<p>Device is busy processing RPC request</p><p></p>|
### <a name="_toc138179096"></a>Share Attribute

|***Key***|**Description**|
| -: | :- |
|*s.sys.epochsec*|<p>EPOCH time in second. The system Real time clock can be updated by the server through this key.</p><p></p>|
|*s.sys.mqttsenddelay*|Minimum period between 2 consecutive MQTT Packet sending. This is to prevent packet sending too fast causing MQTT broker to drop packet. Value 100~1000 (millisecond).|

### <a name="_toc138179097"></a>RPC Call and Response

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*r.sys.reboot*|Boolean|<p>Reboot the device</p><p></p>|


# <a name="_toc138179024"></a><a name="_toc138179098"></a>Limitation and Counter Measure of MQTT server
Due to the nature of the TCP communication protocol used by the MQTT server, and the turnaround time required by the MQTT server to process an incoming TCP packet, a delay between sending two consecutive TCP packets from the device must be provided. 

User can configure the delay period from 100~1000ms by setting the attribute “s.sys.mqttsenddelay”.

` `If the device generates multiple JSON messages between the sending period, the JSON messages will be cached in the device memory until the next sending time slot. All the cached JSON messages will be combined and sent out in one TCP packet.

If the backend Application Server is monitored the topic to received messages from the device, the Application Server will receive multiple JSON messages one big chuck.

















![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.028.png)For the Application Server to properly Deserialize the JSON messages, the received message must first go through a splitter module to split out the JSON messages one by one and Deserialize it accordingly.


# <a name="_toc138179099"></a>The Device Peripheral – RFID Reader
## <a name="_toc138179100"></a>RFID Reader Peripheral

|***Key***|**Value**|
| -: | :- |
|*keycmd*|uhfrfid|
|*feature*|NA|

### <a name="_toc138179101"></a>Attribute
#### *Device Only Attribute*

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*d.uhfrfid.ch*|Integer|<p>Indicate number of available RFID Channel</p><p></p>|
|*d.uhfrfid.pwrmax*|Integer|<p>Maximum reader power in dBm</p><p></p>|
|*d.uhfrfid.pwrmin*|Integer|<p>Minimum reader power in dBm</p><p></p>|
|*d.uhfrfid.csmax*|Integer|<p>Maximum Tag Cache Memory size (in number of tag)</p><p></p>|
|*d.uhfrfid.antstate*|Array of Boolean|<p>Each element indicates if the antenna channel is detected connect to external antenna.</p><p>Eg. [true,false,true,true], indicate that Antenna Channel 1,3,4 is connected with antenna and channel 2 is NOT connected with antenna. </p><p></p>|
|*d.uhfrfid.antison*|Array of Boolean|<p>Each element indicated if the antenna output channel is ON (true) or OFF (false).</p><p>Eg. [true,false,true,true}, indicate that Antenna Output Channel 1,3,4 is ON and channel 2 OFF.</p><p></p>|
|*d.uhfrfid.temp*|Integer|<p>RFID reader internal temperature in degree Celsius.</p><p>Temperature must not exceed 85°C. Once it reached 85°C, it will force the reader to stop the tag detection to prevent system from overheating.</p><p></p>|
|*d.uhfrfid.readerver*|String|<p>Internal RFID Reader Module Firmware ID</p><p></p>|


#### *Share Attribute*
The function of the Share Attribute can be categories as below,

- Tag Inventory and Cache Setting 
- Tag Reading Mode Setting
- Reader Setting
- Demo and Testing
#### *Tag Inventory and Cache Setting*
Configuration of the reading behavior, timing and triggering during tag inventory process.

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*s.uhfrfid.devreadperiod*|Integer|<p>Period in millisecond for the device to read for the tag in the multi tag reading loop. Once the tag reading is started, within the period, the reading process cannot be interrupted. The device will only return after finished the period. The setting range is 500ms to 10000ms.</p><p></p>|
|*s.uhfrfid.auto*|Boolean|<p>False : </p><p>Will only start Tag Inventory/Reading upon request (r. uhfrfid.start=true) and stop when reach s.uhfrfid.period</p><p>True : </p><p>Will continue Tag Inventory/Reading when r.uhfrfid.start=true and stop when r.uhfrfid.start=false.</p><p></p><p>Please noted if it is set to True, the reader will start the Tag Inventory/Reading process immediately after the system is power up.</p><p></p>|
|*s.uhfrfid.period*|Integer|<p>Reading period in second when s. uhfrfid.auto=false.</p><p>Value: 5sec ~ 300sec</p><p></p>|
|*s.uhfrfid.inptrig*|Boolean Array|<p>Enable(True) or Disable(False) Input trigger from on board input port to start the Tag reading/inventory process when the s.uhfrfid.auto=false.</p><p>E.g. “s.uhfrfid.inptrig” : [true,false] with enable input port#0 to start the Tag reading/inventory process.</p><p></p>|
|*s.uhfrfid.cachetagremove*|Boolean|<p>If true, will auto remove the tag from the cache memory after the period given by s.uhfrfid.cacheperiod.</p><p>If false, the tag data will still in the cache memory until the tag inventory process is stop by calling r.uhfrfid.start=false or the reader stop when reading period is over during s.uhfrfid.auto=false.</p><p>No more new tag will be added into the cache once the cache memory is full.</p><p></p>|
|*s.uhfrfid.cacheperiod*|Integer|<p>Period for the detected tag to be stay in the Tag Cache Memory before remove it from the cache. After a tag is detected, if the tag is still staying in the reader reading range, the same tag will be re-detected again. As long as the re-detected period is less than the cache period, the tag will not be removed from the cache. The system will only update the tag info in the Telematics topic when the tag detected is newly detected and not already available in the Tag Cache Memory. </p><p></p><p>Value provided is millisecond.</p><p>Value=500ms to 60000ms</p><p>This setting only valid if s.uhfrfid.cachetagremove=true.</p><p></p>|
|*s.uhfrfid.tagremoveupd*|Boolean|<p>When set to True, it will send out the tag information when the tag is no more detected and remove from the cache memory.</p><p></p>|
|*s.uhfrfid.antChangeUpd*|Boolean|<p>Enable(true)/Disable(false).</p><p>When enabled, it will send out the detected tag in Telematics if the tag is reading from different antenna channel.</p><p>If it is disable, it will only send out the detected tag info ONCE when it is detected irrespective of the of the antenna channel.</p><p></p>|
|*s.uhfrfid.enbforceupd*|Boolean|<p>When set to true, the system will send out the tag info that currently in the cache memory. The period is depend on the setting in s.uhfrfid.forceupdperiod</p><p></p>|
|*s.uhfrfid.forceupdperiod*|Integer|<p>Range 3~100Second = period in force update tag info in the cache memory. Only valid if s.uhfrfid.enbforceupd=true.</p><p></p>|


#### *Tag Selection/Singulation Filter Criteria*
While the system is reading/inventory the surround tag, the system is able to filter off the unwanted tag and only read the tag that matching the selection filter criteria.

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*s.uhfrfid.selfilteroption*|Integer 0~4|<p>Tag Selection mode.</p><p>0 = Disable Tag Selection Filter (Any surrounding detected tag will be selected, rest of the key not required)</p><p>1 = Tag Selection Filter with Tag EPC. (key “s.uhfrfid.selfilteraddr” is not used)</p><p>2 = Tag Selection Filter with data in TID Memory Bank</p><p>3 = Tag Selection Filter with data in USER Memory Bank</p><p>4 = Tag Selection Filter with data in EPC Memory Bank</p><p></p>|
|*s.uhfrfid.selfilteraddr*|32bit Hex String|<p>Define the starting bit address in the Tag Memory to compare with the s.uhfrfid.selfileterdata. If bit address is 0x20, it will have value “20”.</p><p>Please refer to RFID Tag Memory Map Layout. </p><p></p>|
|*s.uhfrfid.selfilterlenbit*|Integer|<p>Specified number of BIT to compare/match during tag filter selection</p><p></p>|
|*s.uhfrfid.selfilterdata*|String of Hex Byte, Max 64byte|<p>Define the data to be compared against the data in the Tag memory. </p><p>The system will start to match/compare from the MSB bit for the first byte and total bit to compare is according to s.uhfrfid.selfilterlenbit.</p><p></p>|
|*s.ufhrfid.selfilterinvert*|Boolean|<p>If set to True, it will select the Tag that **NOT** matching the tag selection filter criteria.</p><p></p>|

For more information on the Tag Selection/Singulation filter criteria, please refer to section “Tag Selection Filter”.
#### *Auto Tag Data Reading*
While the system is inventory /reading the surround tag, the system is able to read one of the memory banks in the tag to allow fast acquiring of the tag data. 

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*s.uhfrfid.enbtagdata*|Boolean|<p>Enable Tag Data reading during Inventory process. When enabled, the system will auto read the data from one of the memory bank (RESERVED, EPC, TID, USER).</p><p></p>|
|*s.uhfrfid.tagdatamembank*|Integer 0~3|<p>Part of Enable Tag Data Reading Setting. Specified the memory bank to be read,</p><p>0 = RESERVED</p><p>1 = EPC</p><p>2 = TID</p><p>3 = USER</p><p></p>|
|*s.uhfrfid.tagdatareadaddr*|32bit Hex String|<p>Part of Enable Tag Data Reading Setting. Set the start address (16bit addressing) of the tag memory to read. </p><p>Eg. If Bit Address of the Tag Memory is 0x20, the s.uhfrfid.tagdatareadaddr will be set to “2”. </p><p></p>|
|*s.uhfrfid.tagdatawordcount*|Integer 1~96|<p>Part of Enable Tag Data Reading Setting. Set the total number of words (16bit) to read.</p><p></p>|
|*s.uhfrfid.enbtagpass*|Boolean|<p>Enable(true)/Disable(false) Tag password during tag inventory</p><p></p>|
|*s.uhfrfid.tagpass*|32Bit Hex  String|<p>32Bit Tag password in Hex String.</p><p>Eg. “ff2d2050” will have 0xff,0x2d,0x20,0x50 as tag password.</p><p></p>|

When turning on the tag data reading, if the tag is lock with password, the s.uhfrfid.enbtagpass must be set to True with s.uhfrfid.tagpass having the tag password.

If the tag data is read successfully, it will return together with other tag information in the Telematics Data with the key “tagdata”. Please refer to the Telematics Data section t.uhfrfid.param for more information.
#### *Tag Reading Mode Setting*
Various reader reading tuning values are available to allow fast reading of the surrounding tag according to the various environment condition and application requirement.

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*s.uhfrfid.dynamicq*|Boolean|<p>When true(1), the Q factor is set to Dynamic Q and the s.uhfrfid.q setting will be ignore</p><p></p>|
|*s.uhfrfid.q*|Integer|<p>Tag Query Q factor 0~16 (default = 4), Higher Q value suitable high tag density detection but with slower return respond.</p><p>If the factor is -1, the Dynamic Q factor is enabled.</p><p></p>|
|*s.uhfrfid.semode*|Integer|<p>Set the Tag Query Session mode to S0~S3 </p><p>Value: 0 to 3</p>|
|*s.uhfrfid.target*|Integer 0~3|<p>0 = Target A. Read ‘A’ tag and move it to state ‘B’.</p><p>1 = Target B. Read ‘B’ tag and move it to state ‘A’.</p><p>2 =Target A-B. Reads ‘A’ tags one at a time and moves them into the ‘B’. Once no more tag found, start to beads ‘B’ tags one at a time and moves them into the ‘A’ state. The process with repeat again and again.</p><p>3 = Target B-A. Same as Target A-B but in reverse order.</p><p></p>|
|*s.uhfrfid.epcextended*|Boolean|<p>Enable(true)/Disable(false) EPC Extended Info.</p><p>When enabled, the tag ID provided in the Telematics will have format as below,</p><p></p><p>PC(2byte)+EPC+CRC(2byte)</p><p></p><p>PC – Protocol Control Word</p><p>EPC – Tag EPC Memory, word size is depend on the PC word setting.</p><p>CRC – Tag CRC Word calculate by the tag.</p><p></p>|


#### *Reader Setting*

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*s.uhfrfid.antenb*|Array of Integer|<p>Auto Detect, Enable and Disable the Antenna Output Channel. </p><p>During Auto mode, the device will enable the antenna channel when antenna is detected on the antenna port.</p><p>When is set to Enable, it will force enable the antenna channel without checking the present of the antenna on the antenna port. </p><p>If it is set to Disable, the antenna channel will be disable.</p><p>0=Auto, 1=Enable, 2=Disable. </p><p>\*\* Enable the antenna output channel without antenna connected to the port will damage the antenna output port.</p><p>E.g. {0,0,2,2} will set Antenna CH1 and 2 to auto mode, 3 and 4 to Disable.</p><p></p>|
|*s.uhfrfid.power*|Array of double|<p>Set each antenna output power in dBm, range 1dbm to 33dbm. </p><p>Eg. [28,30,30,30], will set Antenna Channel 1 to 28dBm and Antenna Channel 2,3,4 to 30dBm.</p><p>The power is in 1dBm step.</p><p></p>|

#### *Demo and Testing*

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*s.uhfrfid.demo*|Boolean|<p>When set to true, all the detected tag will be immediately posted out in the Telemetry Topic. Internal cache will always clear.</p><p></p>|



### <a name="_toc138179102"></a>Telematics Data

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*t.uhfrfid.param*|Array of object|<p>Return the tag detected/undetected result. Each element of the array will contain key/value as below,</p><p>- tag : UHF Tag EPC data in format <PC+EPC+CRC> display in hex string.</p><p>- ch :  Antenna Channel number where the tag is detected. The Channel number starting from 1.</p><p>- rssi : is the tag data return signal strength indicator</p><p>- ts : is the system time stamp since power up in millisecond.</p><p>- state : integer 0,1,2.</p><p>&emsp;- 0 = the previously detected tag is no more detected and has been remove from cache memory.</p><p>&emsp;- 1 = tag is newly detected and add into the cache.</p><p>&emsp;- 2 = resend the tag info that currently in the cache memory.  </p><p>- tagdata : return the tag data if s.uhfrfid.enbtagdata is enable and the tag data is successfully read.</p><p></p>|
|*t.uhfrfid.readstarted*|Boolean|<p>True if the reading is started.</p><p>False if the reading has stopped.</p><p></p>|
|*t.uhfrfid.temp*|Integer|<p>RFID reader internal temperature in degree Celsius. Temperature must not exceed 85°C. Once it reached 85°C, it will force the reader to stop the tag detection to prevent system from overheating.</p><p></p>|
|*t.uhfrfid.temperr*|Boolean|<p>Set to true if the RFID reader internal temperature is 85C and above. (Over temperature error)</p><p></p>|
|*t.uhfrfid.antstate*|Array of Boolean|<p>Will sent out when antenna connected status is changed. Each element indicates if the antenna channel is detected connect to external antenna.</p><p>Eg. [true,false,true,true], indicate that Antenna Channel 1,3,4 is connected with antenna and channel 2 is NOT connected with antenna. </p><p></p>|
|*t.uhfrfid.antison*|Array of Boolean|<p>Will sent out when antenna connected status is changed. Each element indicated if the antenna output channel is ON (true) or OFF (false).</p><p>Eg. [true,false,true,true}, indicate that Antenna Output Channel 1,3,4 is ON and channel 2 OFF.</p><p></p>|
|*t.uhfrfid.writetag*|JSON Object|<p>Return the Tag Writing request result code.</p><p>The Object will contain key below,</p><p>“writeoption”, The last request tag writing option</p><p>“code”, The result code in 16bit Hex string, Please refer to section “TAG Reading/Writing Return Code” for more info.</p>|
|*t.uhfrfid.readtag*|JSON Object|<p>Return the Tag Writing request result code.</p><p>The Object will contain key below,</p><p>“readoption”, The last request tag writing option</p><p>“code”, The result code in 16bit Hex string. Please refer to section “TAG Reading/Writing Return Code” for more info.</p><p></p><p></p>|

#### *Example of a telematics packet*
![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.029.png)


### <a name="_toc138179103"></a>RPC Call and Response
#### *Tag Inventory/Auto reading*

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*r.uhfrfid.start*|Boolean|<p>True</p><p>- Start the reading process. </p><p>- If s.uhfrfid.auto=true, it stop reading when it reach the s.uhfrfid.period setting.</p><p>- Clear the Tag Cache memory to allow new tag info to be updated in the telematics topic.</p><p>False</p><p>- Immediate stop detecting the card</p><p></p><p>Return result in RPC Call Response</p><p>r.uhfrfid.result = true if the command process successfully.</p><p></p>|
|*r.uhfrfid.reload*|Boolean|<p>Will flush the internal cache to and rescan all the tag.</p><p>Set to True only.</p><p>This command only allow when the reader is currently reading tag.</p><p></p>|

##### Example of the RPC Request,
![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.030.png)
##### Example of the RPC Reply
Below is the respond in RPC Reply topic once the reader has started the Tag Inventory/Reading process,

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.031.png)


#### *Tag Writing*
The RFID Tag writing include,

- Writing on one tag at a time.
- Optional tag selection filter according to data in any memory bank.
- Writing on tag memory bank RESERVED, EPC, TID and USER with user definable writing data size and address location in the tag memory.
- Tag writing data must be in multiple of 16bit.
- Set the Tag Locking flag on individual memory bank.
- Kill the RFID Tag and prevent the tag from further reading. Once the tag is killed, it will not respond to any RFID reading request.

All the Tag Writing request will be put under key value “r.uhfrfid.writetag” JSON object. The parameter require for the Tag Writing request will be placed under this key value. The Tag Writing request can be done when the reader is idling or while the reader is on Tag Inventory/Reading mode.

If the Tag Writing request command provided fulfill the parameter requirement and accepted for processing, it will respond with result = TRUE in RPC Reply Topic. The request will be queue for processing. Once the request is processed, the processed result will be returned in Telematics Topic under key “t.uhfrfid.writetag”.

If the system currently busy or the request command provided does not fulfill the parameter requirement, it will respond with result = FALSE.

For more information on the Tag Writing telematics result, please refer to “t.uhfrfid.writetag” under “Telematics Data” Section.

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*r.uhfrfid.writetag*|JSON Object|<p>All the parameter require will be place under this JSON object</p><p></p>|

##### Parameter in key “r.uhfrfid.writetag” JSON object

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*writeoption*|<p>Integer</p><p>0~6</p>|<p>Tag Writing process available option are,</p><p>0 = Write to RESERVED memory bank</p><p>1 = Write to EPC memory bank </p><p>2 = Write TID memory bank</p><p>3 = Write USER memory bank</p><p>4 = Replace Tag EPC (will direct replace existing EPC and update PC and CRC in the tag)</p><p>5 = Lock Tag memory</p><p>6 = Kill Tag</p><p></p>|
|*timeout*|Integer, 16bit|<p>Optional. Tag writing time out in millisecond. Default is set to 1000ms if it is not provided.</p><p></p>|
|*tagselection*|JSON object|<p>Optional. JSON object that provides the tag selection/filter criteria when writing the tag. If not provided, it will write to all the surrounding detected tag.</p><p>For further detail, please refer to the Parameter in key “tagselection” JSON object at table below.</p><p></p>|
|*writeaddr*|32bit Hex String|<p>Set the start address (16bit addressing) of the tag memory to write. </p><p>E.g. If Bit Address of the Tag Memory is 0x20, the writeaddr will be set to “2”. Please refer to RFID Tag Memory Map Layout for the bit addressing.</p><p>Require by writeoption 0, 1, 2, 3</p><p></p>|
|*writedata*|<p>String of Hex Byte</p><p>Max 32 words</p>|<p>Data byte to write on the tag, require by writeoption 0, 1, 2, 3.</p><p>Must be in 16bit words for writeoption 0,1,2,3. Max 32 words.</p><p>On writeoption 0, 1, 2, 3, The Tag writing will be in multiple of 16bit words. The Hex string provided will be auto zero padded to fulfill the requirement.</p><p></p>|
|*lockmask*|16bit Hex String|<p>Lock tag Mask Word Setting</p><p>Require by writeoption=5 only.</p><p>Refer to Section “Tag Locking and Tag Password” for further detail.</p><p></p>|
|*lockaction*|16bit Hex String|<p>Lock tag Action Work setting.</p><p>Require by writeoption=5 only.</p><p>Refer to Section “Tag Locking and Tag Password” for further detail.</p><p></p>|
|*password*|32bit Hex String|<p>Tag password for the tag writing operation. Do not provide if no password is set for the tag.</p><p>When writeoption is 0~4, it is the Access Password (optional).</p><p>When writeoption is 5, it is the Access Password (required)</p><p>When writeopting is 6, it is the Kill Password (required)</p><p></p>|

##### Parameter in key “tagselection” JSON object

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*option*|Integer 0~4|<p>Tag Selection mode.</p><p>0 = Disable Tag Selection Filter (Any surrounding detected tag will be selected, rest of the key not required)</p><p>1 = Tag Selection Filter with Tag EPC. (key “addr” not required)</p><p>2 = Tag Selection Filter with data in TID Memory Bank</p><p>3 = Tag Selection Filter with data in USER Memory Bank</p><p>4 = Tag Selection Filter with data in EPC Memory Bank</p><p></p>|
|*addr*|32bit Hex String|<p>Define the starting address in the Tag Memory to compare with the key “data”. If bit address is 0x20, it will have value “20”.</p><p>Please refer to RFID Tag Memory Map Layout for the memory addressing. </p><p></p>|
|*lenbit*|Integer|<p>Specified number of BIT to compare/match during tag filter selection. The bit is compare starting from the MSB.</p><p></p>|
|*data*|String of Hex Byte, Max 64byte|<p>Define the data to be compared against the value in the Tag memory. </p><p>The system will start to match/compare from the MSB bit for the first byte and total bit to compare is according to key “lenbit”.</p><p></p>|
|*invert*|Boolean|<p>Optional Key. If set to True, it will select the Tag that **NOT** matching the tag selection filter criteria. If not provided, will be default to false.</p><p></p>|


Below is some of the writing request examples.
###### Example 1, Replace Tag’s EPC without Password
![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.032.png)This example will cause the reader to replace the tag EPC with “EA000001”. Since no Access password is provide, the Tag EPC bank should not be locked. Due to the Selection Filter is not provided, the reader will select any one of the tags detected by the reader. Once the command is accepted, the reader will return “result” = True in RPC Reply Topic.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.033.png)Once the command is accepted and finish processed, the system will return the write request result in the Telematic Topic. If the writing into the tag is successful, it will return “code”:”0000”.




###### ![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.034.png)Example 2, Replace EPC with Access Password
` `This example will cause the reader to replace the tag EPC with “EA000001” with the Tag access password set to “11112222”. 

The Tag’s EPC Memory bank must be in locked condition prior to calling this write request.

###### Example 3, Replace Kill/Access Password
![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.035.png)Since tag selection filter (“tagselection”) is provided and the total bit to check with the tag EPC (“option” = 1) is 32 bit (“lenbit” = 32, which is 4byte), the reader will only select tag with EPC = ”EA000001”. Once tag is found, the reader will write the value from “writedata” (Total 4 words), into the Tag’s RESERVED Bank starting from address 0x00 without providing access password (The Tag’s RESERVED Memory Bank is not locked)

As the Kill password memory location is at Bit address 0x00 and Access password memory location is at address bit address 0x10 (refer to section Tag Locking and Tag Password), this JSON RPC request will effectively replace the Kill password with hex value “aaaabbbb” and Access password with hex value “11112222”.  The password is 32bit (4byte).

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.036.png)
###### Example 4, Lock Tag’s EPC Memory Bank
This Command will Lock the Tag’s EPC Memory bank Write access. The Access Password is require and must be the same value with the value in the Tag’s RESERVED Bank Access password.

Due to the selection option, it will only write to the tag having EPC=”EA000001”.

After this command, any tag writing request to the Tag’s EPC Memory Bank, will require to provide the Access Password.

###### ![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.037.png)Example 5, Kill Tag
This RPC Request will select the tag having EPC = “EA000001” and send the Kill tag command with the Kill Password = “aaaabbbb” to the tag.

Once the kill tag command is successfully executed, the tag will no long usable. It will not respond to and reader request anymore.





#### *Tag Reading*
The RFID Tag reading include,

- Reading on one tag at a time.
- Optional tag selection filter according to data in any memory bank.
- Reading on tag memory bank RESERVED, EPC, TID and USER with user definable writing data size and address location in the tag memory. Maximum number of bits on each read is 96 words (1536bits)
- Tag reading data must be in multiple of 1 word(16bit).

Parameter require for the Tag Reading request will be placed under key value “r.uhfrfid.readtag” JSON object. The Tag Reading request can be done when the reader is idling or while the reader is on Tag Inventory/Reading mode.

If the parameter of Tag Reading request command provided fulfill the requirement and accepted for processing, it will respond with result = TRUE in RPC Reply Topic. After that, the request will be queue for processing. Once the request is processed, the processed result will be returned in Telematics Topic under key “t.uhfrfid.readtag”.

If the system currently busy or the request command provided does not fulfill the parameter requirement, it will respond with result = FALSE.

For more information on the Tag Reading telematics result, please refer to “t.uhfrfid.readtag” under “Telematics Data” Section.

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*r.uhfrfid.readtag*|JSON Object|<p>All the parameter require will be place under this JSON object</p><p></p>|

##### Parameter in key “r.uhfrfid.writetag” JSON object

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*readoption*|<p>Integer</p><p>0~3</p>|<p>Tag Writing process available option are,</p><p>0 = Read to RESERVED memory bank</p><p>1 = Read to EPC memory bank </p><p>2 = Read TID memory bank</p><p>3 = Read USER memory bank</p>|
|*timeout*|Integer, 16bit|<p>Optional. Tag writing time out in millisecond. Default is set to 1000ms if it is not provided.</p><p></p>|
|*tagselection*|JSON object|<p>Optional. JSON object that provides the tag selection/filter criteria when writing the tag. If not provided, it will write to all the surrounding detected tag.</p><p>For further detail, please refer to the Parameter in key “tagselection” JSON object at “Tag Writing -> Parameter in Key tagselection”.</p><p></p>|
|*readaddr*|32bit Hex String|<p>Set the start address (16bit addressing) of the tag memory to read. </p><p>E.g. If Bit Address of the Tag Memory is 0x20, the readaddr will be set to “2”. Please refer to RFID Tag Memory Map Layout for the bit addressing.</p><p></p>|
|*wordcount*|<p>Integer</p><p>1~96</p>|<p>Number of word(16bits) to read. Maximum 96words.</p><p></p>|
|*password*|32bit Hex String|<p>Tag’s Access password for the tag reading operation if the tag is locked. Do not provide if no password is set for the tag.</p><p></p>|

####### ![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.038.png)*Example 1: Reading any surround tag*
The device will start to read any first detected data. It will read the EPC Memory Bank, starting from Word Address 0x0, total word to read is 5 words.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.039.png)

Once the parameter provided is confirmed fulfill the requirement, it will send out the confirm packet in the RPC response topic.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.040.png)If the reading is successful, it will return the reading result in the Telematic Topic with code=”0000” together with the tag data requested.




####### ![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.041.png)*Example 2: Reading Tag with Selection Filter*
This command will only select and read tag with Tag EPC=”EA000001”. It will read the tag’s User Memory Bank starting from Word Address 0x0, and will total 5 words (10bytes)



### <a name="_toc138179104"></a>RFID Tag Memory Map Layout
![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.042.png)

The Tag contain 4 type of Memory bank, Reserved, EPC, TID and USER. The addressing for the memory in each bank is according to BIT addressing. 

E.g., The EPC data for the tag is located at Bank 01 (EPC) starting from address 0x20. Please take note that Address 0x20 will be BIT15 of the EPC data and Address 0x2F will be BIT0 of the EPC data.

The default addressing method shown in the memory map above is based on bit addressing. Each memory bank has its own bit addressing and all of them is starting from bit address 0x00.

As for Word addressing, each Word has 16bit. Example Word addressing conversion from bit addressing are as follow,

`	`Bit address 0x00 = Word address 0x00

`	`Bit address 0x10 = Word address 0x01

`	`Bit address 0x20 = Word address 0x02

When reading or writing into the Tag memory, it will be done in multiple of 16bit only.


## <a name="_toc138179105"></a>Tag Selection/Singulation
The reader allows the user to configure the Tag Selection/Singulation Filter according to the parameter provided during the Tag Inventory/Reading process and Tag writing process (with RPC Request).

The tag selection can be based on criterial below,

- Compare the filter byte provided with any memory location in the 4-memory bank or with the Tag’s EPC.
- Compare any number of bits with the filter byte provided.
- Invert the selection to select the Tag that does NOT fulfill the criterial provided.
### <a name="_toc138179106"></a>Example
The selection criteria requirement are as below,

- Compare the filter byte provided with EPC Memory Bank starting from bit address = 0x20.
- Total number of bits to compare is 4 bits.
- The filter byte provided is 0x80.

The attribute setting for the reader during Tag Inventory/Reading are as below,

|*Attribute setting for Tag Inventory/Reading*|*RPC Request under “tagselection” during Tag Writing Request*|*Value*|*Value Type*|
| :- | :- | :- | :- |
|s.uhfrfid.selfilteroption|option|4|Integer|
|s.uhfrfid.selfilteraddr|addr|“20”|Hex String|
|.uhfrfid.selfilterdata|data|“80”|Hex String|
|s.uhfrfid.selfilterlenbit|lenbit|4|Integer|
|s.ufhrfid.selfilterinvert|invert|false|Boolean|

` `With the setting above, the device will only compare the first 4 bits of the Filter data with the EPC Memory bank starting from bit address 0x20 to 0x23.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.043.png)
## <a name="_toc138179107"></a>Tag Locking and Tag Password
Locking the EPC Gen2 tag will require to set the access password to none zero and set the locking state of each memory bank (Perma-Lock/Perma-Unlock Bit and Write Lock Bit).
### <a name="_toc138179108"></a>Gen2 Tag Passwords
An EPC Gen2 tag has two separate passwords, an Access Password and a Kill Password, each are 32 bits and are stored in the reserved bank (bank 00) of the tag memory. Both of the password can be separately lock from future reading and writing.

Access Password is used when the reader tries to read/write to the tag that having the Access Password already set in the RESERVER Bank.

![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.044.png)Kill Password is required when the reader want to kill/disable the tag. Once the tag is killed, the tag is no more accessible from any RFID reader.

### ![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.045.png)<a name="_toc138179109"></a>Lock Mask and Lock Action

1. R/W = Access Password Read and Write Lock
1. W = Access Password Write Lock
1. Perm = Perma-Lock (1)/Perma-Unlock (0)

When the Bit number in the Mask Word is set to 1, the correspondent bit’s function in the Action Word will be processed.

E.g., If Mask Word is 0x0020 and Action Word is 0x0020, EPC Bank will be Write Locked.
### <a name="_toc138179110"></a>Tag Locking State Chart
The possible locking state of the tag by setting the Perma bit and W(R/W) bit, the are listed below,

||**W (R/W) = 0**|**W (R/W) = 1**|
| :- | :-: | :-: |
|<p></p><p></p><p>**Perma = 0,**</p><p>**(Perma-unlocked)**</p>|You can read and write the EPC memory and you can change the protection status. This is not recommended.|<p>You can read the memory zone (If it is R/W Lock, reading also require access password), but in order to write it, you must provide the access password. This means that the memory zone is password write protected. You can also change the protection status. This is the preferred way to reversibly unlock the EPC memory.</p><p></p>|
|<p></p><p></p><p>**Perma = 1,**</p><p>**(Perma-locked)**</p>|Under this condition the EPC memory will be always writeable (and readable) and this status cannot ever be changed. There is no way to write protect the EPC memory.|<p>You can read the memory zone, but you can never write it again. You will never be able to change the protection status. This is the preferred way to perma-lock the memory zone.</p><p></p>|

The Perma bit can only set **ONCE** only. Once it is set, it cannot be clear.

As long as Perma bit is **NOT** set, the R or R/W bit can be set or clear. But if the Perma bit is set, the R or R/W bit cannot be change any more.
### <a name="_toc138179111"></a>Tag Locking process
The step to lock the tag are as below,

1. Write a 32bit non-zero Access Password and Kill Password.
1. Program the data into the memory bank that need to be locked.
1. Lock the memory bank and the Access and Kill password memory to prevent reading of the access password and kill password.

Please note that only reserved memory bank (Access and Kill Passwords) can be both READ and WRITE locked - all others (EPC, TID, and User) can be write-locked only. Typically, the Tag Identification (TID) memory bank is perma-locked at the factory during tag manufacturing.


## ![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.046.png)<a name="_toc138179112"></a>Tag Reading Process


During the Tag reading process, the Tag info detected by the Impinj Reader Chipset will only be send out the MCU Cache memory when reached the end of the s.uhfrfid.devreadperiod period.

The Tag information will stay in the cache for the period of s.uhfrfid.cacheperiod. If the same Tag is detected before reaching the end of the period, the tag time stamp will be reset. The tag will only be removed from the cache tag when it reached the end of the cache period.

When the tag is first added into the cache, the tag information will be sent out in JSON format to the backend system (through MQTT server or serial port).

When the tag is removed from the cache memory, if s.uhfrfid.tagremoveupd is set to true, the tag information will be sent out in JSON format to the backend system too.

When reading is stop, all the Tag information in the cache memory will be deleted silently.


## <a name="_toc138179113"></a>TAG Reading/Writing Return Code

|*Error Code*|*Description*|
| -: | :- |
|*0000*|Operation Success|
|*0100*|Write Data Length Error|
|*0105*|Parameter Error|
|*0400*|No Tag Detected|
|*040A*|Tag Writing Error|
|*0420*|GEN2 Other Error|
|*0423*|Tag Memory Overrun, Bad PC|
|*0424*|Memory Locked Unable to Write|
|*042B*|Insufficient Power|
|*042F*|Non Specific Error|
|*0430*|Unknow Error|
|*0504*|Reader Over Temperature|
|*0505*|Standing Wave Ratio/Reflection too large|
|*f000*|Command Sent Error|
##
# <a name="_toc138179114"></a>The Device Peripheral – Output Port
## <a name="_toc138179115"></a>Output Port Peripheral

|***Key***|**Value**|
| -: | :- |
|*keycmd*|outputport|
|*feature*|2ch (indicating the device have 2 Ch Output Port)|

### <a name="_toc138179116"></a>Attribute
#### *Device Only Attribute*

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*d.outputport.ch*|Integer|Indicate number of available output Channel|

#### *Share Attribute*

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*s.outputport.setup*|Array of object|<p>Define the on state of each channel, each element will contain value as below,</p><p>{</p><p>`   `“ch”: 0,</p><p>`   `“onishigh”:true,</p><p>`   `“mode”: 0,</p><p>`   `“fperiodon”: 3,</p><p>`   `“fperiodoff”: 1,</p><p>`   `“pulsecnt: 1</p><p>}</p><p>- ch, Channel index</p><p>- onishigh, if set to true, it will turn on the internal MOSFET/Switch when “ison” is true. </p><p>- mode, output port mode. Available option are, </p><p>&emsp;- 0, Standard output mode</p><p>&emsp;- 1, Pulse output mode</p><p>- fperiodon, on pulse width period in 100ms per count during Pulse Mode</p><p>- fperiodoff, off pulse width period in 100ms per count during Pulse Mode</p><p>- pulsecnt, number of on/off cycle during pulse mode.</p><p>The total period of each on/off cycle will be,</p><p>Cycle Period = “fperiodon” + “fperiodoff”</p><p></p>|


### <a name="_toc138179117"></a>Telematics Data

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*t.outputport.param*|Array of object|<p>Return the status of each port in the array if the status of the array changes. Each element of array will consist of value listed below,</p><p>{</p><p>“ch”: 0,</p><p>“ison”: true</p><p>“ts”: 342352</p><p>}</p><p>Where,</p><p>- ch, is the port channel index.</p><p>- ison, set to true if it is on and false when it is off.</p><p>- ts, system time stamp in millisecond</p><p></p>|

### <a name="_toc138179118"></a>RPC Call and Response

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*r.outputport.param*|Array of Object|<p>Set the output port. Each element in the array will be consist of,</p><p>{</p><p>“ch”: 0,</p><p>“ison”: true,</p><p>}</p><p></p><p>Where,</p><p>- ch, is the channel index.</p><p>- ison, set to true of false, for further detail, please refer below for Standard Mode and Pulse Mode.</p><p> </p><p>During Standard mode, set “ison” to true will turn on the output, set it to false will turn it off.</p><p></p><p>During Pulse mode, set “ison” to true will start the pulse output. </p><p></p><p>During the output port is sending out the output pulse, </p><p>- If “ison” is set to true again, it will reset and restart the pulse counting internal counter and continue with the pulse output.</p><p>- If “ison” is set to false, it will immediately stop the pulse output and set the output port to off.</p><p></p><p>Return result in RPC Call Response</p><p>r.outputport.result = true if the command process successfully.</p><p></p>|



![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.047.png)

Using High Power N-Channel MOSFET as Switch.

Please take note that the output port is not suitable to direct drive high current inductive load. If driving high current inductive load is require, please isolate the output with a relay.



# <a name="_toc138179119"></a>The Device Peripheral – Input Port
## <a name="_toc138179120"></a>Input Port Peripheral

|***Key***|**Value**|
| -: | :- |
|*keycmd*|inputport|
|*feature*|2ch (indicating the device have 2 Ch Output Port)|
### <a name="_toc138179121"></a>Attribute
#### *Device Only Attribute*

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*d.inputport.ch*|Integer|Indicate number of available input Channel|

#### *Share Attribute*

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*s.inputport.setup*|Array of object|<p>Define the on state of each channel, each element will contain value as below,</p><p>{</p><p>`   `“ch”: 0,</p><p>`   `“onishigh”:false,</p><p>`   `“mode” : 0,</p><p>`   `“debounce”: 10</p><p>}</p><p>- ch (Must provide) = Channel index </p><p>- onislow (optional) = if true, on will be during the input is in LOW state.</p><p>- Mode (optional) = Input port mode, </p><p>&emsp;- 0 = Push Button Mode, Push Button input that will publish out once when the switch is press/pushed.</p><p>&emsp;- 1 = normal input port that publish out the on/off state when input port changes the state.</p><p>- debounce (optional) = debounce delay count index. The higher the index, the longer the device delay. Value = 2 to 50 (default 10). Only available when Mode=0 (button input mode)</p><p></p>|


### <a name="_toc138179122"></a>Telematics Data

|***Key***|**Value Type**|**Description**|
| -: | :- | :- |
|*r.inputport.param*|Array of object|<p>Return the status of each port in the array. Each element of array will consist of value listed below during Mode=0,</p><p>{</p><p>“ch”: 0,</p><p>“ison”: true,</p><p>“ts”: 34245324,</p><p>“count”: 554</p><p>}</p><p>- ch = Input Channel Index.</p><p>- ison = true if it is on and false when it is off.</p><p>- ts = System timestamp in millisecond.</p><p>- count = number of On/Off cycle count. Add 1 when the input turn from off to on.</p><p>If the Mode=1 (Button Mode), the Status return will be in format below for each input,</p><p>` `{</p><p>“ch”: 0,</p><p>“btnpress”: 1,</p><p>“ts”: 34245323,</p><p>“count”: 554</p><p>}</p><p>- ch = Input Channel Index.</p><p>- ts = System timestamp in millisecond.</p><p>- btnpress can be either </p><p>&emsp;- 1 for normal press, </p><p>&emsp;- 2 for double click the button, </p><p>&emsp;- 3 for triple click the button, </p><p>&emsp;- 4 for long press for more than 4~5 second.</p><p>- count = number of button press cycle count according. Add 1 on each button press.</p><p></p>|


### <a name="_toc138179123"></a>RPC Call and Response
N/A



![](Aspose.Words.6785d622-dcda-4463-bb04-87784adc7989.048.png)




**49 **|** Page

