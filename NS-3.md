# NS-3

## Definition
NS or the network simulator is a discrete event network simulator. It is popular in academia for its extensibility (due to its open source model) and plentiful online documentation. NS is popularly used in the simulation of routing and multicast protocols, among others, and is heavily used in ad-hoc networking research. NS supports an array of popular network protocols, offering simulation results for wired and wireless networks alike. 

NS-3 is a discrete-event network simulator for Internet systems, targeted primarily for research and educational use. ns-3 is free, open-source software, licensed under the GNU GPLv2 license, and maintained by a worldwide community.

## Features
The ns-2 simulator has been a popular tool for research and education in Internet and network systems for many years. However, work is progressing on a replacement for ns-2, which borrows concepts and implementations from various open-source simulators such as ns-2, YANS, and GTNetS. NS-3 has several diffenrences from NS-2, including:
* New software core: Designed to improve scalability, modularity, coding style, and documentation, the core is written in C++ but with an optional Python scripting interface (instead of OTcl). Several C++ design patterns such as smart pointers, templates, callbacks, and copy-on-write are leveraged. Object aggregation capabilities enable easier model and packet extensions.
* Attention to realism: The Internet nodes are designed to be a more realistic representation of real computers, including the support for key interfaces such as sockets and network devices, multiple interfaces per nodes, use of IP addresses, and other similarities.
* Software integration: Architecture to support the incorporation of more open-source networking software such as kernel protocol stacks, routing daemons, and packet trace analyzers, reducing the need to port or rewrite models and tools for simulation.
* Support for virtualization: Lightweight virtual machines running over a (possibly wireless) simulation network are an attractive combination for current research; ns-3 plans to support a few modes of such operation including a native “process” environment where Posix-compliant applications can be easily ported to run in simulation space with their own private stack, and including support for tying together virtual machines of various types.
* Testbed integration: Ns-3 will enable the testbed-based researcher to experiment with novel protocol stacks and emit/consume network packets over real device drivers or VLANs. The internal representation of packets is network-byte order to facilitate serialization.
* Attribute system: Researchers require a means to identify and possibly reassign all values used to configure parameters in the simulator. Ns-3 provides an attribute system that integrates the handling and documentation of default and configured values.
* Tracing architecture: Ns-3 is building a tracing and statistics gathering framework using a callback-based design that decouples trace sources from trace sinks, enabling customization of the tracing or statistics output without rebuilding the simulation core.
* Topology: For ease of use, a number of stock topology objects should be predefined. These stock objects can be instantiated by a single line of C++ code constructing the object, with configurable arguments. Stock objects should include trees, meshes, stars, and random topologies of arbitrary size. They have incorporated such topology objects from GTNetS. 

## Code Architecture
NS-3 code is divided into different parts. First, we start with topology definition and then we define models to use, after that we configure over model by giving them some addresses and setting other parameters, and finally we executed the code. The output which is generated in trace format will be analysed with some tools like Wireshark. The procedure of code creation is shown in the figure
![image](https://hackmd.io/_uploads/HkKe5kxRA.png)


## Installation
Steps to install NS-3:
* Install dependencies
`sudo apt-get install build-essential g++ python mercurial` 
![image](https://hackmd.io/_uploads/rJJiiJe0C.png)

* Clone NS-3 all in one from repository
`git clone https://gitlab.com/nsnam/ns-3-allinone.git`
![image](https://hackmd.io/_uploads/H161RJlC0.png)


* Download all the program
`cd ns-3-allinone/`
`python3 download.py`
![image](https://hackmd.io/_uploads/ryFtAJxC0.png)

* Build the program
`python3 build.py --enable-examples --enable-tests`
![image](https://hackmd.io/_uploads/HknZtgg00.png)
![image](https://hackmd.io/_uploads/HkgQtxg0R.png)
![image](https://hackmd.io/_uploads/r1Rx-vxCR.png)


* Test the NS-3
`python3 test.py`
![image](https://hackmd.io/_uploads/SJTabve0R.png)
![image](https://hackmd.io/_uploads/B1TuIDgRA.png)

All of the tests passed, it means that the NS-3 works well

## Running NS-3 Program
We will run several NS-3 programs to test the functionality of the NS-3:
### Example point to point topology
This is the topology:
![image](https://hackmd.io/_uploads/SksU-DWCA.png)
This is the code from the example program for point to point topology
![image](https://hackmd.io/_uploads/SJwqq8-RR.png)
In this code:
* We enable the built-in logging from UDP Echo client and server
* We create 2 nodes and install a point to point channel between the nodes
* We set IPv4 for both of the nodes
* We set the second node as a UDP echo server and the first nodes as 
UDP echo client
* We run the simulator

To run the simulator, we use these commands:
`./ns3 build`
`./ns3 run scratch/example.cc`

The result is this:
![image](https://hackmd.io/_uploads/rJ6vnLZC0.png)
![image](https://hackmd.io/_uploads/BJ3d2LZA0.png)

From the result, we can conclude that the point to point link is succesfully build and the client can sent UDP package which are replied by the server. 

### Example point to point topology with CSMA
This is the topology:
![image](https://hackmd.io/_uploads/B1XtbDW0R.png)
This is the code from the example program for point to point topology with CSMA
![image](https://hackmd.io/_uploads/ryf0-DZ0C.png)
![image](https://hackmd.io/_uploads/ry9yzP-RA.png)

In this code:
* We enable the arguments from cmd to specify the number of CSMA devices and to enable logging
* We create 2 nodes and install a point to point channel between the nodes
* We create a csma nodes on the second devices and a number of csma nodes based on the argument (default number is 3 nodes)
* We assign the 2 nodes with IP address with base "10.1.1.0/24"
* We assign the csma nodes with IP address with base "10.1.2.0/24"
* We set the last node of the csma as a UDP echo server and the first node (from the point to point) as UDP echo client
* We run the simulator

To run the simulator, we use these commands:
`./ns3 build`
`./ns3 run scratch/second.cc`

The result is this:
![image](https://hackmd.io/_uploads/By5s7PWRR.png)


From the result, we can see that the last node of the csma (with IP address 10.1.2.4) become the UDP echo server and the UDP echo client (with IP address 10.1.1.1) succesfully sends UDP package and replied by the server.

CSMA (Carrier Sense Multiple Access) is a technique used by devices which utilize a shared medium for communication. In this topology, n0 and n1 create a point to point link, and n2, n3, n4 create a link with the n1 node, which create a LAN (local area network) with CSMA.

In my understanding, this topology is analogous to a typical network topology with a router, switch, and devices connected to the switch:
* n0 (Router): n0 can be described as a device that functioning like a router, connecting the point-to-point link (example WAN or another network) to the LAN (CSMA network).
* n1 (Switch): n1 serves as a switch in the CSMA LAN. It connects n2, n3, and n4 in the LAN, allowing them to communicate with each other and with n0 through the point-to-point link.
* n2, n3, n4 (End Devices): These nodes can be considered as end devices connected to the switch, such as PCs or server

### Example point to point topology with Wi-Fi and CSMA
This is the topology:
![image](https://hackmd.io/_uploads/rJzEjozAA.png)

This is the code from the example program for point to point topology with Wi-Fi and CSMA:
![image](https://hackmd.io/_uploads/By4YjsMCA.png)
![image](https://hackmd.io/_uploads/Hk3cisGCR.png)



In this code:
* We enable the arguments from cmd to specify the number of CSMA devices and the number of STA devices
* We create 2 nodes and install a point to point channel between the nodes
* We create a Wi-FI Access Point (AP) on the first device (n0) and a number of STA devices based on the argument (default number is 3 devices)
* We create a csma nodes on the second device (n1) and a number of csma nodes based on the argument (default number is 3 nodes)
* We assign the 2 nodes with IP address with base "10.1.1.0/24"
* We assign the csma nodes with IP address with base "10.1.2.0/24"
* We assign the Wi-Fi network with IP address with base "10.1.3.0/24"
* We set the last node of the csma (n4) as a UDP echo server and the last device of the Wi-FI network (n7) as UDP echo client
* We run the simulator

To run the simulator, we use these commands:
`./ns3 build`
`./ns3 run scratch/example3.cc`

The result is this:
![image](https://hackmd.io/_uploads/ry146jG0R.png)

To be able to create a Wi-Fi network, we must:
* Configures the Wi-Fi channel using `YansWifiChannelHelper`
* Configures MAC layers for STA and AP devices using `WifiMacHelper`
* Assigns mobility models to the Wi-Fi devices using `MobilityHelper`. The STAs move within a rectangular boundary, while the AP has a fixed position

Additionally, we can also see the animation of our created topology simulation using NetAnim. NetAnim is an offline animator based on the Qt toolkit, it can be combined with NS-3. To animate the simulation we must:
* Add NetAnim Module to the code
`#include "ns3/netanim-module.h"`
* Before the simulation in the code, add code to export the simulation into XML file.
`AnimationInterface anim("Animation.xml");`
![image](https://hackmd.io/_uploads/SyweQ3MR0.png)

* Run NetAnim
`cd ../netanim`
`./NetAnim`
![image](https://hackmd.io/_uploads/ryzSm2fCA.png)
![image](https://hackmd.io/_uploads/BkyImnMC0.png)

* Open the exported XML file and press play to run the animation.
![image](https://hackmd.io/_uploads/HywumnGC0.png)

It will run the animation from the topology simulation before

## Enable Python Binding in NS-3
NS-3 also have capabilities to add python binding, so that we can write simulation scripts based on python. Steps to enable python binding in NS-3:
* Install cppyy, cppyy version must be 3.1.2 to be able to work with ns-3 3.42
`pip3 install cppyy==3.1.2`
![image](https://hackmd.io/_uploads/S11kyr40R.png)
* Configure NS-3 
`./ns3 configure --enable python-bindings`
![image](https://hackmd.io/_uploads/HJ8FeS4RC.png)
![image](https://hackmd.io/_uploads/Sk5eWBEAR.png)

Test the python bindings:
* Copy example python file
`cp examples/tutorial/first.py scratch/example1.py`

* Build the NS-3
`./ns3 build`
![image](https://hackmd.io/_uploads/SkmHMHEAA.png)

* Run the python file
`./ns3 example1.py`
![image](https://hackmd.io/_uploads/HkrosS4R0.png)

The NS-3 successfully run simulation using python file.

## Conclusion
NS-3 is an active open-source project and open-source development model, several simulator features designed to aid current Internet research, community-based development and maintenance model, trying to avoid some problems with ns-2, such as interoperability and coupling between models, lack of memory management, debugging of split language objects. 

## References
A. Mohta, S. I. Ajankar, and M. M. Chandane, ‘Network Simulator-3: A Review’