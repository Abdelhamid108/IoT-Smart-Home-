# IOT smart home

#📘 Smart Home: Living Room — Network Simulation
#📝 Overview
This project simulates a Smart Home - Living Room environment using Cisco Packet Tracer, focusing on the integration of IoT devices, wireless connectivity, and basic automation. It demonstrates how various smart devices can interact within a LAN, managed by a central home gateway, and controlled via a remote access solution or home automation dashboard.

#🧱 Topology Summary
The topology consists of the following main components:

Device Type	Quantity	Purpose
Home Gateway	1	Provides routing, DHCP, and wireless access.
Smart Devices	4+	Smart lamp, smart fan, motion sensor, etc.
Generic Laptop/PC	1–2	Controls, monitors, and configures devices.
Smartphone/Tablet	1	Mobile control and monitoring.
Cloud/Server	Optional	Remote access or external control simulation.

#🔌 Connectivity
Wireless Communication is used to link IoT devices to the Home Gateway.

Devices use IPv4 DHCP for address assignment (via the Home Gateway).

Control center (PC/laptop) is connected via Ethernet or Wi-Fi.

The smartphone is connected wirelessly to demonstrate mobile control.

#📱 Smart Devices Used
These devices are typically found in the simulation:

Smart Lamp – Can be turned on/off remotely.

Smart Fan – Controlled based on temperature or manual settings.

Motion Sensor – Detects movement and triggers actions (e.g., lights).

Thermostat – Monitors and adjusts room temperature.

Door Sensor or Camera – For security purposes (if included).

#🛠️ Configuration Steps
Setup Home Gateway:

Configure DHCP to assign IPs to IoT devices.

Enable Wireless with SSID and security (e.g., WPA2).

Connect Smart Devices:

Set SSID on each device.

Ensure each device gets an IP from the gateway.

Automation Scripts (Optional):

Use the "Event Planning" tab in devices to schedule actions.

Example: Motion Sensor triggers the lamp.

PC/Tablet Configuration:

Open the IoT Monitor or Controller App.

Link devices for real-time status and control.

#🤖 Automation Examples
If motion detected, then turn on light for 1 minute.

If temperature > 30°C, then turn on fan.

Scheduled events: Turn off all devices at midnight.

#🌐 Remote Access (Optional)
Simulate internet access via a cloud object.

Configure port forwarding on the Home Gateway to allow smartphone control from outside.

#💡 Educational Purpose
This simulation is designed to:

Demonstrate basic IoT principles.

Practice wireless configuration and IP addressing.

Learn about smart automation and event-driven actions.

Understand device communication within a LAN.
