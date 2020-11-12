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
6. Optional Set-up Node-MCU

# Step 1 Do some shopping (Optional)

I used for this code pattern the following components:



* *Keyestudio smart home set*: https://www.amazon.com/KEYESTUDIO-Starter-Electronics-Automation-Education/dp/B08CZ778DJ/ref=sr_1_3?dchild=1&keywords=Keyestudio+Smart+Home+Kit&qid=1605176281&sr=8-3 , this includes a laser cut wooden house, with an Arduino clone with a sensor shield, bluetooth board, sensors and actuators. This is available on Amazon but also at Ali-express etc. It is really good quality, with excellent instructions to build the house and to connect everything together. The needed code is available online. For every sensor/actuator is code available, and ofcourse also for the complete set-up.

* *Raspberry PI 1*: This house is connected to a gateway, I used a Raspbery Pi 4 for that, but can also be a 3. This Raspberry acts as a gatway between the devices and the MQTT server. This gateway is also connected to the cloud or local machine. OPTIONAL: you can also run this on another device, like your local machine.

* *Raspberry Pi 2*:  This raspberry acts as a MQTT Broker I used a Raspbery Pi (3 or 4) for that with a sense-hat board. This sensehat is optional, I use it for displaying traffic going through the MQTT server. OPTIONAL: you can also use a public broker for this, or run a broker on another device.

* Web camera, this can be any USB camera or a Raspberry Pi camera.

* OPTIONAL: *NodeMCU*: there are different devices based on ESP8266, It is open source and relatively cheap and easy to work with. I am using a LoLin board, which has wifi on board, I have connected some sensors to it to control my 'smart garden'


For this code pattern I used different pieces of hardware. To use all the possibilities I am going to mention in this Code pattern I advise you to have all parts available. You can also follow this code pattern with only having an Arduino with one sensor. All the parts running on the 2 Raspberry Pi's can also run on your laptop. 

