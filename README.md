# Open source tools to Connect and control your ‘Smart home’ via MQTT and Bluetooth
Sometimes it can be complicated to read certain sensors to see what is going on. In this code-pattern that is made simple, with only open-source technologies. This might not be an enterprise ready solution, but it show how easy it is to use any device. So also more professional devices can be used in similar ways.

When you have completed this code-pattern, you will understand how to:

*	Connect sensors and actuators to an Arduino and read their values
*	Set up a gateway on a Raspberry Pi
*	Run a MQTT Server on a Raspberry Pi
*	Connect sensors on a NodeMCU device and read their values
*	Build an application in Node-RED
*	Use Bluetooth, Wifi and MQTT (and optional LoRAWan) to communicate between the devices

## Flow
 
1.	The home consists of a lot of sensors and actuators connected to an Arduino clone
2.	The smart garden, which is a NodeMCU-device with some sensors to control the garden
3.	Both devices are connected to a gateway, which sends and receives data, This is based on a raspberry pi
4.	The smarthome is also connected to a mobile device via Bluetooth
5.	Via MQTT a Nod-RED dashboard is connected to the gateway
6.	This dashboard can be reached by mobile devices via WiFi and gives more information then in step4
7.	A camera is connected to the gateway to automatically take pictures when someone approaches the smart home

## Included Components
* Node-RED
* MQTT
* Bluetooth
* Arduino
* Raspberry Pi
* Sensors
* Actuators
* Slack
