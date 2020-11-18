# Open source tools to Connect and control your ‘Smart home’ via MQTT and Bluetooth
Sometimes it can be complicated to read certain sensors to see what is going on. In this code-pattern that is made simple, with only open-source technologies. This might not be an enterprise ready solution, but it show how easy it is to use any device. So also more professional devices can be used in similar ways.

When you have completed this code-pattern, you will understand how to:

*	Connect sensors and actuators to an Arduino and read their values
*	Set up a gateway on a Raspberry Pi
*	Run a MQTT Server on a Raspberry Pi
*	Connect sensors on a NodeMCU device and read their values (Optional)
*	Build an application in Node-RED
*	Use Bluetooth, Wifi and MQTT (and optional LoRAWan) to communicate between the devices
* Send messages to Slack

## Flow
 
1.	The home consists of a lot of sensors and actuators connected to an Arduino clone
2.	The smart garden, which is a NodeMCU-device with some sensors to control the garden (optional)
3.	Both devices are connected to a gateway, which sends and receives data, This is based on a raspberry pi
4.	The smarthome is also connected to a mobile device via Bluetooth
5.	Via MQTT a Nod-RED dashboard is connected to the gateway
6.	This dashboard can be reached by mobile devices via WiFi and gives more information then in step4
7.	A camera is connected to the gateway to automatically take pictures when someone approaches the smart home and send to Slack

## Included Components

* Node-RED, Open source flow based editor to create applications
* MQTT, open source protocol for sending messages
* Bluetooth
* Arduino, open source micro processor
* Raspberry Pi, credit card sized mini computer
* Sensors: Gas sensor, humidity sensor, light sensor, movement sensor,
* Actuators: LED's, fan, servo's, buttons, relay, LED display
* Web camera
* Slack
* Optional: Node-MCU, microprocessor

# Featured technologies

* Node.js
* C++ for Arduino and Node-MCU

# Prerequisites

* Node.js installation (with NPM)
* Arduino IDE + libraries
* Familiarity with basic Arduino concepts
* Familiarity with basic Node-RED concepts
* Familiarity with basic Linux concepts

# Steps

Follow these steps to setup and run this code pattern. The steps are described in detail below.

1. Do some shopping (optional)
2. Clone the repo
3. Build your smart home and set up application
4. Set up MQTT Broker
5. Set up Gateway
6. Send data via Gateway
7. Optional Set-up Node-MCU

# Step 1 Do some shopping (Optional)

I used for this code pattern the following components:



* *Keyestudio smart home set*: https://www.amazon.com/KEYESTUDIO-Starter-Electronics-Automation-Education/dp/B08CZ778DJ/ref=sr_1_3?dchild=1&keywords=Keyestudio+Smart+Home+Kit&qid=1605176281&sr=8-3 , this includes a laser cut wooden house, with an Arduino clone with a sensor shield, bluetooth board, sensors and actuators. This is available on Amazon but also at Ali-express etc. It is really good quality, with excellent instructions to build the house and to connect everything together. The needed code is available online. For every sensor/actuator is code available, and ofcourse also for the complete set-up.

* *Raspberry PI 1*: This house is connected to a gateway, I used a Raspbery Pi 4 for that, but can also be a 3. This Raspberry acts as a gatway between the devices and the MQTT server. This gateway is also connected to the cloud or local machine. OPTIONAL: you can also run this on another device, like your local machine.

* *Raspberry Pi 2*:  This raspberry acts as a MQTT Broker I used a Raspbery Pi (3 or 4) for that with a sense-hat board. This sensehat is optional, I use it for displaying traffic going through the MQTT server. OPTIONAL: you can also use a public broker for this, or run a broker on another device.

* Web camera, this can be any USB camera or a Raspberry Pi camera.

* OPTIONAL: *NodeMCU*: there are different devices based on ESP8266, It is open source and relatively cheap and easy to work with. I am using a LoLin board, which has wifi on board, I have connected some sensors to it to control my 'smart garden'


For this code pattern I used different pieces of hardware. To use all the possibilities I am going to mention in this Code pattern I advise you to have all parts available. You can also follow this code pattern with only having an Arduino with one sensor. All the parts running on the 2 Raspberry Pi's can also run on your laptop. 

# Step 2 Clone the repo

First let's get the code. From the terminal of the system you plan on running Node-RED from, do the following:

Clone the XXXXXX repo:

$ git clone https://github.com/IBM/xxxxxxxxx
Move into the directory of the cloned repo:

$ cd xxxxxx
Note: For Raspberry Pi users, details on accessing the command line can be found in the remote access documentation if not connecting with a screen and keyboard.

# Step 3 Build your smart home and set up application

here you can find all instructions to build the smart home: https://wiki.keyestudio.com/KS0085_Keyestudio_Smart_Home_Kit_for_Arduino

You first get an introduction of all the part of the complete set. Then you start with downloading the Arduino software, needed to program the micro controller. The instructions are based for a Windows, but instructions for Mac are similar.

DRIVER FOR MAC NEEDED?? CHECK

Then to check if you can connect with the Arduino, you use a example skech to test connectivity.

Next step is to install needed libraries for two of the components: LED display and the servo's. After doing this, you are good to go!

The tuturial then continues with a description of all the components and some sample code to test. there is also a good explanation of the every peace of code available.

The last step before assembling the wooden house and the components, is to connect your IOS or Android device to the Bluetooth Module. You have to dowhnlaod an app, with this app you can control and start/stop some of the components. Later on in this code pattern you will build an alternative for this.

If the house is assembled, you need to connect all the wires from the components to the expansion board, in the tutorial you will see a table to connect the components to the right ports. When this is done, it is time to upload the code to control all the components, which is available in the last step of the tutorial.

When the sketch is uploaded, you can test all the different compenents one by one to see if they are connected in the right way.

FYI, I did not connect the servo from the window in the right way: it opens when the water sensor gets activated....

# Step 4 Set up MQTT Broker

MQTT is a lightweight and simple messaging protocol. therefore you need a braker which recieves and sends messages based on a certain topic. If you want to read more about MQTT, please go here: https://mqtt.org
In this step I used a Raspberry Pi for an MQTT Broker. You can also host it locally on your laptop or use a test-broker as found on the web.
I used Mosquito as this is the most used on Raspberry, but basically you can use any broker.

to install, use the following command: ```sudo apt install mosquitto mosquitto-clients```

Start the broker and  automatically start after reboot using the following command:-
```
sudo systemctl enable mosquitto
```
The broker should now be running. You can check this via the systemd service status:-
```
sudo systemctl status mosquitto
```
The output should be similar as the following:
```
pi@rpiMqttServer:~ $ sudo systemctl status mosquitto
● mosquitto.service - LSB: mosquitto MQTT v3.1 message broker
   Loaded: loaded (/etc/init.d/mosquitto; generated; vendor preset: enabled)
   Active: active (running) since Thu 2020-11-12 13:17:10 CET; 4 days ago
     Docs: man:systemd-sysv-generator(8)
  Process: 331 ExecStart=/etc/init.d/mosquitto start (code=exited, status=0/SUCCESS)
    Tasks: 1 (limit: 4915)
   CGroup: /system.slice/mosquitto.service
           └─444 /usr/sbin/mosquitto -c /etc/mosquitto/mosquitto.conf

Nov 12 13:17:07 rpiMqttServer systemd[1]: Starting LSB: mosquitto MQTT v3.1 message broker...
Nov 12 13:17:10 rpiMqttServer mosquitto[331]: Starting network daemon:: mosquitto.
Nov 12 13:17:10 rpiMqttServer systemd[1]: Started LSB: mosquitto MQTT v3.1 message broker.
```
Now it is time to test the broker. Therefor you need to subscribe to an MQTT topic.

A topic is simply a string that looks like a file system path. It has the general form:-

a/b/c/...

The great thing about MQTT is that you can just make up topics which describe your needs. You don’t need to register them anywhere. In this test we use ```test/message```
In the existing terminal, subscribe to the test/message topic:

```mosquitto_sub -h localhost -t "test/message"```

This will send a  message to the MQTT broker which is currently running on the same system (-h localhost option). But it could be running somewhere else.


Because your current terminal is listening to the topic, you willneed to open another terminal. 

Once open, publish message to the test/message topic like this:-

``` mosquitto_pub -h localhost -t "test/message" -m "Hello, world" ```
If you look back at the first terminal now you should see this:-

```Hello, world```

if this works, your MQTT Broker is working!

Optional:

I added a sensehat (https://www.raspberrypi.org/products/sense-hat/?resellerType=home)to the raspberry Pi to make it visual when messages are being send. Every time a messasege goes through the broker, an image is being diplayed on the sensehat.

An application in Node-RED is made for that, you can find the FLow here: xxxxxx
<< explain flow here >>

# Step 5 Set up Gateway

# 6 Send data via Gateway

# 7 Optional Set-up Node-MCU

# Links

## License

This code pattern is licensed under the Apache License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1](https://developercertificate.org/) and the [Apache License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache License FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)

