# Quick Setup Guide (TU-04-C04)

**Industrial IoT UHF RFID Fix Reader**

Please install Android App below from Google Play Store to start configuring your device.

[WiRiO3 Device Configurator Google Play Store](https://play.google.com/store/apps/details?id=com.wirio3.wifi_provision)

![Apps QR](../picture/Wirio3%20Apps%20PlayStore%20Link%20small.png)

To quickly setup the device through the android app, Press the "Conf" button once to allow the device to go into configuration mode, 

![Device Config Button](picture/FWBus%20Conn%20device-ConfigButton.png)

Once the configuration mode is started, the Link Indicator LED will turn to "Blink-Twice".

Further detail on the device configuration using Android App, please refer link below,

[Device Configuration With WiRiO3 Device Configurator Guide (PDF)](pdf/WiRIO3%20Device%20Configuration%20Manual.pdf)

# Power Supply

The RFID Reader can be power up either through the POE Ethernet Connection or direct DC power supply. For direct DC power supply input the device can support supply voltage range from DC 12V up to DC 24V. The power requirement is 15W.

Please take note that the power supply from the USB connector **DO NOT** have enough power to power up the RFID Reader. If the USB is connected without power supply source either from POE or DC Input, the device will reboot due to insufficient power provided.

![FWBus Wiring Layout](picture/FWBus%20Conn%20device-Connector.png)

# Extending the I/O port

The RFID Reader's I/O port allow to be extended thought FWBus located at the "Port" connector with Remote I/O Extension (Model: RE-01-0808) . Each RE-01-0808 have 8 channel of output port and 8 channel of Input port. Each RFID Reader can support up to 8 unit of RE-01-0808 make the total number of I/O port become 64 channel of Output port and 64 channel of Input port.

When connecting the RE-01-0808 I/O Extension unit, please make sure that the DeviceID of each Extension unit is unique and set according to ID 0 to ID 7 through the DIP switch on the Extension unit.

![FWBus Conn Device](picture/FWBus%20Conn%20device-Connect%20RE-01.png)

DIP Switch setting on the I/O Extension Unit.

![RE-01 DIP Switch](../doc_RE01/picture/RE-01%20DeviceID%20Dip%20Switch.png)

# Other document
[Device Specification](TU04-Device_Spec.md)

[Device Specification (PDF)](pdf/TU-04-C04 Product Specification.pdf)

[WiRIO3 Basic Communication Specification](../WiRIO3%20Comm%20Spec/WiRIO3%20MQTT%20Base%20Communication%20Spec/README.md)

[Device Specific Communication Specification](../WiRIO3%20Comm%20Spec/TU04C04/README.md)
