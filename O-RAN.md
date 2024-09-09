# O-RAN (Open Radio Access Network)

## Definition
O-RAN (Open Radio Access Network) is a new paradigm for the RAN, where the deployment are based on disaggregated, virtualized and software-based components, connected through open and well defined interfaces, and interoperable across different vendors. Previously, RAN components were monolithic units, all-in-one solutions that implement each and every layer of the cellular protocol stack. They were provided by a limited number of vendors and seen by the operators as black-boxes. 

Disaggregation and virtualization enable flexible deployments, based on cloud-native principles. This increases the resiliency and reconfigurability of the RAN. Open and interoperable interfaces also allow operators to onboard different equipment vendors, which opens the RAN ecosystem to smaller players. Finally, open interfaces and software-defined protocol stacks enable the integration of intelligent, data-driven closed-loop control for the RAN. 

The O-RAN Alliance is an industry organization created in 2018 with the goal of implementing these principles on top of 3GPP LTE and NR RANs. Specifically, the O-RAN Alliance embraces and extends the 3GPP NR 7.2 split for base stations. The latter disaggregates base station functionalities into a Central Unit (CU), a Distributed Unit (DU), and a Radio Unit (RU). Moreover, O-RAN connects them to intelligent controllers through open interfaces that can stream telemetry from the RAN and deploy control actions and policies to it.

## Main Principles
There are 4 main principles of the O-RAN, which are disaggregation,  intelligent, data-driven control with the RICs, virtualization and open interfaces

### Disaggregation
RAN disaggregation splits base stations into different functional units. The gNB is split into a Central Unit (CU), a Distributed Unit (DU), and a Radio Unit (RU) (called O-CU, O-DU, and O-RU in O-RAN specifications). The CU is further split into two logical components, one for the Control Plane (CP), and one for the User Plane (UP). This logical split allows different functionalities to be deployed at different locations of the network, as well as on different hardware platforms. For example, CUs and DUs can be virtualized on white box servers at the edge, while the RUs are generally implemented on Field Programmable Gate Arrays (FPGAs) and Application-specific Integrated Circuits (ASICs) boards and deployed close to RF antennas. 

The O-RAN Alliance has evaluated the different RU/DU split options proposed by the 3GPP, with specific interest in alternatives for physical layer split across the RU and the DU. The selected 7.2x split strikes a balance between simplicity of the RU and the data rates and latency required on the interface between the RU and DU. In split 7.2x:
* The RU performs time-domain functionalities, with precoding, Fast Fourier Transform (FFT), cyclic prefix addition/removal, and Radio Frequency (RF) operations, which makes the RU inexpensive and easy to deploy. 
* The DU then takes care of the remaining functionalities of the physical layer, and of the Medium Access Control (MAC) and Radio Link Control (RLC) layers
* The CU units (CP and UP) implement the higher layers of the 3GPP stack, i.e., the Radio Resource Control (RRC) layer, which manages the life cycle of the connection; the Service Data Adaptation Protocol (SDAP) layer, which manages the Quality of Service (QoS) of the traffic flows (also known as bearers; and the Packet Data Convergence Protocol (PDCP) layer, which takes care of reordering, packet duplication, and encryption for the air interface, among others.

![image](https://hackmd.io/_uploads/SyWV4mn20.png)


### RAN Intelligent Controllers and Closed-Loop Control
RAN Intelligent Controller introduce programmable components that can run optimization routines with closed-loop control and orchestrate the RAN. The O-RAN data pipeline the O-RAN stream and aggregate hundreds of Key Performance Measurements (KPMs) on the status of the network infrastructure (e.g., number of users, load, throughput, resource utilization). The O-RAN has two logical controllers that process this data and leverage AI and ML algorithms to determine and apply control policies and actions on the RAN.  Effectively, this introduces data-driven, closed-loop  control that can automatically optimize, for example, network and RAN slicing, load balancing, handovers, scheduling policies, among others.

The two logical controllers of the O-RAN are the Non-real-time RIC and Near-real-time RIC
* The non-real-time (or non-RT) RIC is a component of the Service Management and Orchestration (SMO) framework which  operates on a time scale longer than 1 s. The non-RT RIC provides guidance, enrichment information, and management of ML models for the near-RT RIC. Additionally, the non-RT RIC can influence SMO operations which gives the non-RT RIC the ability to indirectly govern all the components of the O-RAN architecture connected to the SMO, thus making decisions and applying policies that influence thousands of devices
* Near-real-time RIC and Control Loop: The near-real-time
(or near-RT) RIC is deployed at the edge of the network and operates control loops with a periodicity between 10 ms and 1s. The near-RT RIC interacts with DUs and CUs in the RAN and usually associated to multiple RAN nodes, thus the near-RT closed-loop control can affect the QoS of hundreds or thousands of User Equipments (UEs). The near-RT RIC consists of multiple applications supporting custom logic, called xApps, and of the services that are required to support the execution of the xApps
* An xApp is a microservice that can be used to perform radio resource management through specific interfaces and service models. It receives data from the RAN and (if necessary) computes and sends back control actions.
![image](https://hackmd.io/_uploads/rJmfKQ3hR.png)

###  Virtualization
The O-RAN architecture introduces additional components for the management and optimization of the network infrastructure and operations, spanning from edge systems to virtualization platforms. All the components of the O-RAN architecture can be deployed on a hybrid cloud computing platform called O-Cloud. Specifically, the O-Cloud is a set of computing resources and virtualization infrastructure that are pooled together in one or multiple physical datacenters. This platform combines physical nodes, software components, and management and orchestration functionalities,
and specializes the virtualization paradigm for O-RAN

The virtualization for the RAN components and of the O-RAN compute elements is expected to introduce savings and optimization of the power consumption related to the RAN. Virtualization makes it possible to easily and dynamically scale up or scale down the compute resources required to support user requirements, thus limiting the power consumption to the actual network functions that are needed
![image](https://hackmd.io/_uploads/ryuL572hA.png)


###  Open Interfaces
Finally, the O-RAN Alliance has introduced technical specifications that describe open interfaces connecting a number of different components of the O-RAN architecture. The O-RAN interfaces, help overcoming the traditional RAN black box approach, as they expose data analytics and telemetry to the RICs, and enable different kinds of control and automation actions, from RAN control to virtualization and deployment optimization.

Standardization of these interfaces is a key step toward breaking the vendor lock-in in the RAN, e.g., allowing a nearRT RIC of one vendor to interact with the base stations of another vendor, or again enabling the interoperability of CUs, DUs and RUs from different manufacturers. This also fosters market competitiveness, innovation, faster update/upgrade cycles, and eases the design and introduction of new softwarized components in the RAN ecosystem

Among the O-RAN-specific interfaces, the E2 interface connects the near-RT RIC to the RAN nodes. E2 enables the near-real-time loops through the streaming of telemetry from the RAN and the feedback with control from the near-RT RIC. The near-RT RIC is connected to the non-RT RIC through the A1 interface, which enables a non-real-time control loop and the deployment of policy, guidance, and intelligent models in the near-RT RIC. The non-RT RIC also terminates the O1 interface, which connects to every other RAN component for management and orchestration of network functionalities

Thanks to the open interfaces, the O-RAN architecture can be deployed by selecting different network locations (cloud, edge, cell sites) for different pieces of equipment, with multiple configurations.

## Reference
M. Polese, L. Bonati, S. D’Oro, S. Basagni and T. Melodia, "Understanding O-RAN: Architecture, Interfaces, Algorithms, Security, and Research Challenges," in IEEE Communications Surveys & Tutorials, vol. 25, no. 2, pp. 1376-1411, Secondquarter 2023, doi: 10.1109/COMST.2023.3239220.
keywords: {Computer architecture;Security;Precoding;3GPP;Radio frequency;Radio access networks;Optimization;Open RAN;O-RAN;cellular;5G;6G},



