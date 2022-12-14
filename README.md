# Simple_Solar_MQTT
This is a basic Arduino C++ demo application using a unique blockchain authenticated MQTT access to receive [Solar.org](https://solar.org/) blockchain events.
This project is designed to run on any ESP32 microcontroller. Blockchain event packets are sent to the serial port as ASCII text for display on terminal program running on PC. Onboard LED is toggled at every blockchain event.

## How to Configure Project

### 1. Create Testnet wallet using [Desktop Wallet](https://solar.org/wallets).
### 2. Request Testnet tokens using [telegram bot](https://t.me/dSXP_bot).
### 3. Vote for Delegate **pj** in Desktop Wallet.
### 4. Create a unique 8 character message and then [sign the message using the desktop wallet](https://friendsoflittleyus.nl/how-to-sign-and-verify-messages-on-solar-blockchain/).
### 5. Rename file **secrets.h_example** to **secrets.h**
### 6. In secrets.h update the following items with your values.
```
#define MQTT_CLIENT_NAME  "random or unique value"  
#define MQTT_USERNAME     "Your Solar Testnet wallet public key"     // Insert your wallet's public key (not the address)	
#define MQTT_PASSWORD     "8 character message + Message Signature"  // Sign any 8 character message to generate signature
  
//WiFi Credentials
#define WIFI_SSID         "Your WiFi SSID"
#define WIFI_PASS         "Your WiFi Password"

//Time Zone Configuration
int8_t TIME_ZONE = -7;    //set timezone:  Offset from UTC
int16_t DST = 3600;       //To enable Daylight saving time set it to 3600. Otherwise, set it to 0. 
```
### 7. Open Simple_Solar_MQTT.ino in Arduino IDE 2.0.1 and add the following libraries
* EspMQTTClient by Patrick Lapointe Version 1.13.3
* ArduinoJson by Benoit Blanchon Version 6.19.4
* PubSubClient by Nick O'Leary Version 2.8

### 8. Edit file in PubSubClient Library to allow for large MQTT data packets.
You need to increase max packet size from 128 to 4096 via this line in \Arduino\libraries\PubSubClient\src\PubSubClient.h
  #define MQTT_MAX_PACKET_SIZE 4096  //default 128

### 9. Selected your specific ESP32 board and Compile/Upload
I am using a Heltec Wireless Stick however any ESP32 board will work.
![PXL_20221117_061046605](https://user-images.githubusercontent.com/33669966/202370553-5e93dbfd-e783-41a0-9806-e433c6fc36dc.jpg)

### 10. Open Serial Port Monitor and change baudrate to 115200

You should see WiFi / MQTT connection messages followed by blockchain events. 

![](https://i.imgur.com/E254o8j.png)
