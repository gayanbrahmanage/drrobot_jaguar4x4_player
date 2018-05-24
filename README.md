# drrobot_jaguar4x4_player H20_motion

(catkin version)

This package provides all the necessary drivers and programs for H20 robot. Initail programs provided by the Dr.Robot Inc have been improved to make the robot more stable in motion. The control program is based on tuned PID controller developed by Robotics and Sensor Group at the University of Calgary, AB, Canada.

## How to install
First, install dependency packages.

### Install joystick 

The driver package for joystick operation can be installed using the following documentation.

[Configuring and Using a Linux-Supported Joystick with ROS](http://wiki.ros.org/joy/Tutorials/ConfiguringALinuxJoystick)

### Install the dependency packages
The H20 driver needs dependency package `DrRobotMotionSensorDriver`
To install, `git clone` the `DrRobotMotionSensorDriver` package to the  directory `catkin_ws/src`

`git clone https://github.com/gayanbrahmanage/DrRobotMotionSensorDriver.git `

source your environment `source devel/setup.bash `

Run `catkin_make`

### Install `drrobot_jaguar4x4_player` from the same directory `catkin_ws/src`

`git clone` to present working directory.

`catkin_ws/src`

## How to run

`roslaunch drrobot_jaguar4x4_player H20base_player_joystick.launch `

`roslaunch drrobot_jaguar4x4_player H20base_player.launch `

### Additional information for data recording
The package can subscribe to the topic `/scan` and publishes the topic `/Rscanpose` that contains `laser scan data`, `pose` and individual `encoder readings` registered at each `timestamp`.

See `rostopic list`


#  Network Setup
(by  Noam Anglo)

###  External Router problem
If the ‘external’ router breaks, you will need to interface somehow with the ‘internal’ access point (in
our case, a PicoStation M2). Get ready for the greatest point-and-click adventure of your life.
Materials needed: an Ethernet cable or two, a new router (obviously) and a computer with Ethernet

###  Key Terms - Basic

Network – a bunch of devices connceted together, usually through Wi-Fi or Ethernet or something

LAN – Local Area Network. Your network. Also refers to a wired Ethernet connection

WAN – Wide Area Network. The Internet

WLAN – refers to a wireless Wi-Fi connection

IP address – a label of a device on some network; is usually assigned within the network. One device
can have several IPs (but usually not)

MAC address – a label of a device that is permanently assigned by the manufacturer. Think of a MAC
address like your name (doesn’t change), and the IP address like your house address (can change if you
move somewhere else, like to a new network). One device has several MAC addresses – one per NIC
NIC – Network Interface Controller. On a laptop, these would be your ethernet controller and your Wi-
Fi controller

DHCP – Dynamic Host Configuration Protocol. A DHCP server will assign IPs to devices connected to
its network that don’t already have a static IP enabled. Without this, you must set your IPs manually
Port – the thing after the IP address, eg. the 8888 in 192.168.0.12:8888. Sometimes you need this.

### Key Terms - Networking Devices

Client – a device that makes requests to a server

Server – a device that takes requests, such as a DHCP server that takes requests for IPs

Switch – a device that acts as a ‘bridge’ or ‘interconnect’ between network devices

AP – Access Point – also called a Wireless Access Point; a device that allows Wi-Fi access to a
network. APs usually have Station functionality.

Station – a device that gives other devices Wi-Fi functionality, i.e. turns them into Wi-Fi clients.
Stations usually have AP functionality.

Router – a device with the combined functionality of a DHCP server, a switch and (in the case of
wireless routers) an AP; also allows for connection to the WAN. Can be configured to act as any one of
these

###  Key Terms – Specific Stuff.

WDS – Wireless Distribution System – allows for a ‘transparent’ connection between two Wi-Fi
devices, as if they were connected over Ethernet

SSID – the “name” of an AP or router’s wireless network

WPA/WEP key – the password into a Wi-Fi network; in the case of WPA, a normal password, and in
the case of WEP, an encryption key. They’re functionally be the same, depending on the type of your
network security

PoE – Power over Ethernet. Lets you provide Power over EthernetStep 1: Set up a suitable replacement router or AP
You’ll need a reasonably modern router, since it has to support WDS and should preferrably support at
least 802.11g. After factory resetting it (or getting into it if you already know its IP, admin username
and password), connect to it via Ethernet (use the LAN port, not WAN) type in its IP in your browser
and log in – check the manufacturer’s websites or the stickers on the back for clues. Configure the
wireless mode to Router mode. Set up an SSID and a WPA/WEP key, depending on if you want to use
WPA2 or WEP. Give it a nice static IP, set its subnet mask to 255.255.255.0, and set its gateway to
192.168.0.1 (unless you know what you’re doing).

In our case... we used a WRT54G2, and set it to WPA2 because I wrote this in 2018 and nobody uses
WEP. Those of you that are highly acquainted with Wi-Fi networks (wait, why are you reading this?)
will note that the WRT54G2 doesn’t have WDS, so we hooked it up to a PicoStation M2 to act as a
WDS AP – pretty much the same configuration, though it’s set to Bridge mode and not Router. For
some reason we couldn’t connect a second wireless device to it so we couldn’t use it by itself.
Step 2: Connect to its Wi-Fi station

There’s two ways to do this – either pop the robot open and connect directly into the Wi-Fi station’s
ethernet (you might need a PoE injector), or use the computer on the front of the robot. Either way
you’ll need to find the station’s IP somehow – if you’re lucky it’s the default on the station
manufacturer’s website, but if not, go look up a tutorial. The basics steps of it are as follows:

- Type in ipconfig for Windows Command Prompt, or ifconfig for Linux Terminal, and check your IP

- Type in your IP with the last number changed to 255 (eg. 192.168.0.255) to ‘broadcast’; might need -b
in Linux

- Wait for the request to time out, or for replies to come in – if it’s a general failure try something else

- Type in arp -a to see the IPs that replied – one of these might be the Wi-Fi station

Afterwards, put its IP in your browser and log in – I hope you know the login info.
In our case... the Wi-Fi station was behind the lower back panel of the robot; it was another
PicoStation M2. We directly connected to it with Ethernet (mostly because it was easy to isolate which
one the station IP was – you couldn’t even see it through the robot computer). The IP was 192.168.0.20,
with the username/password drrobot/drrobot. We figured the latter out purely by guessing.
Step 3: Configure the Wi-Fi station

Hopefully you didn’t reset it (maybe resetting is how we got into this mess in the first place), so it’s
still configured as a WDS Station. Just go to its wireless settings and type in the SSID and WPA/WEP
key of your external router, taking care to match the settings of the two as closely as possible.
In our case... since it was a PicoStation M2, the thing had a “Select” button that listed all the Wi-Fi
networks it detected – it even locked to the MAC address of our router. You still had to change the
security options though.

Step 4: Test
I hope everything works. If your program needs to interface with the robot motors/sensors, for some
reason 192.168.0.95 (and corresponding ports) works regardless of your settings. I don’t know why.
