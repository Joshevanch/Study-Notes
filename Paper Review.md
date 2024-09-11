# Paper Review about Digital Twin Networks for Wi-Fi and 5G/6G O-RAN

Backround theory:
* [O-RAN](https://hackmd.io/@joshevan/HyZCCzn20)
* [Digital Twin](https://hackmd.io/@joshevan/B1LliE3n0)

List of Reviewed papers:
## Colosseum: The Open RAN Digital Twin
M. Polese et al., "Colosseum: The Open RAN Digital Twin," in IEEE Open Journal of the Communications Society, doi: 10.1109/OJCOMS.2024.3447472. keywords: {Open RAN;Digital twins;Radio frequency;Containers;Testing;Software;Protocols;O-RAN;Open RAN;Wireless Network Emulation;5G;6G},



### Background:
* **Needs for Datasets**: To develop robust and scalable Artificial Intelligence (AI) and Machine Learning (ML) solutions for O-RAN, it is necessary to have rich datasets of RAN telemetry, data, and performance indicators. However,  it is often impractical or impossible to use them for research and development due to privacy and security concerns
* **End-to-end AI and ML Testing**. Once trained, AI/ML based control solutions need to be validated and tested in controlled environments to avoid disruption in production networks. At the same time, the testing conditions need to be realistic to be able to represent real-world situations
* **Continuous Software Validation**. While softwarization
introduces flexibility and programmability of the stack, it also comes with concerns around software quality, reliability, security, and performance. Therefore, integrating, validating, testing, and profiling software for wireless in a continuous fashion is key to the Open RAN vision. Additionally, this validation needs to consider various compute platforms and hardware acceleration solutions for physical layer processing
* **Automated Integration and Testing of Disaggregated Components**:  Disaggregation need for the validation of interoperability across vendors and devices. This is a labor-intensive and often manual process that calls for the development of automated techniques

### Proposed Solution: 
* Colosseum—the world’s largest wireless network emulator with hardware in the loop [14]— can be leveraged as a digital twin platform to address these challenges and to develop end-to-end, fully integrated, and reliable solutions for Open RAN
![image](https://hackmd.io/_uploads/rJEtPgv3C.png)
    * Its main components are: 128 pairs of generic compute servers and SDRs, named Standard Radio Nodes, a channel emulation system and a state-of the-art AI/ML infrastructure.
    * Each SDR is paired with a Dell server connected to anNI/Ettus USRP X310 SDR through a dedicated 10 Gbps link
    * The Colosseum channel emulator, namely Massive Channel Emulator (MCHEM), is in charge of reproducing digital representations of real-world RF propagation scenarios, which represent the state of the RF channel at given time instants
    * The AI/ML infrastructure of Colosseum, shown in yellow at the bottom of Figure 1, consists of two NVIDIA DGX A100 stations with 8 GPUs each, providing 10 petaFLOPS of compute power and one Supermicro Superserver 8049U E1CR4T with 6 NVIDIA V100 GPUs and 3 TB of RAM.
* The emulation capabilities of Colosseum can be leveraged to deploy, study, and profile wireless protocol stacks in controlled and repeatable environments

### Capabilities:
* End-to-End Open RAN Twinning in Colosseum
    * Figure 1 showcases the deployment of an end-to-end, fully programmable Open RAN cellular system in Colosseum.
    *  The top-left portion of the figure depicts the RAN, which consists of core network and cellular base station, the top-right The top-right portion of the figure,  shows the Service Management and Orchestration (SMO) and ORAN RICs that interface with the RAN base stations through open interfaces and augment their operations through AI/ML
    *  Colosseum enables experimentation with different open source softwarized protocol stacks, such as OAI for 5G RANs and srsRAN for 4G ones
    *  Users of Colosseum can deploy 5G NR cellular networks on Colosseum through ready-to-use container image
    *  OpenRAN Gym is an open-source framework for O-RAN
experimentation that lets users instantiate softwarized RANs
based on the OAI and srsRAN protocol stacks, and control
them through xApps deployed on an O-RAN Near-Real-time
(RT) RIC. This framework has also been used to demonstrate
the portability of experiments from Colosseum to external
platforms,
* Radio-Frequency Twinning
    * The Colloseum able to The channel and traffic emulation and the cellular protocol stacks, which provide  key components toward the creation of real-time, high-fidelity digital replicas of Open RAN systems with RF hardware in the loop
    * RF Twinning with CaST enables users to characterize real-world RF environments and to turn them into digital twin representations to be used in channel emulators 
![image](https://hackmd.io/_uploads/BkOfagP3C.png)
    * The main steps of CaST scenario creation workflow are as follows: 
    * (i) Identify the wireless environment to capture,i.e., the physical location to twin, which can vary in size andtype, e.g., indoor, outdoor, urban, rural
    * (ii)Obtain the 3D model of the environment by leveraging online databases such as Open Street Map (OSM) or modeling softwaresuch as SketchUp;
    * (iii) Load the model in a ray-tracer, e.g., MATLAB ray-tracer, Wireless InSite (WI), Opal, or Sionna;
    * (iv) Set the location and trajectories of nodes;
    * (v) Sample the channel with the ray-tracer, capturing effects such as mobility of the nodes;
    * (vi) Parse the ray-tracer output to extract the channels for each pair of nodes for each millisecond of the emulated scenario
    * (vii) approximate the resulting channel information in a format suitable for the Colosseum channel emulator
    * (viii) install the scenario in Colosseum, converting it into an FPGA-based format. This scenario creation toolchain is modular, and it allows users to provide their inputs at any of the above-mentioned steps
    * After a scenario is installed in Colosseum, it undergoes validation through the second part of the CaST framework to ensure that it closely follows the expected real-world behavior
    * since Colosseum SDRs are equipped with two transmit-receive chains, Colosseum and MCHEM support 2- by-2 Multiple Input, Multiple Output (MIMO) operations. Thus, CaST can be used to generate simplified MIMO channels leveraging MATLAB or Sionna’s NR 3GPP channel mode
### Use Cases of Colosseum as Open Ran Digital Twin
* **Slicing and Scheduling Optimizatio:** 
    * RAN slicing allows operators to dynamically partition the available spectrum bandwidth to accommodate UEs and traffic with heterogeneous Quality of Service (QoS), performance, and Service Level Agreement (SLA) requirement. 
    * Through the OpenRAN Gym framework, Colosseum provides the tools and infrastructure for data collection, design, training, testing, and evaluation of AI/ML xApps before their deployment on over-the-air deployments
* **Spectrum Sharing:** 
    * Colloseum able to collect a dataset with Wi-Fi and cellular users coexisting in the same frequency band, and to train a detector to identify spectrum usage patterns based on recurrent neural networks

### Experiments
* Access to Colosseum can be requested through a form on its public website
* Colosseum users can interface with Colosseum shared resources through its experiment web portal. On this webpage, users can check resource availability, view lists of scenarios, and manage images and reservations
* Once the SRN reservation is completed and resources become available, users can access their reserved SRNs via SSH and interact with the resources available within each SRN as they would do in a local setup. During the experiment, users can also access the NAS and use the the colosseum-cli utility to manage RF, traffic scenarios
and snapshot the SRN LXC images

### Conclusion:
* This paper reviewed how Colosseum, the world’s largest wireless network emulator with hardware in the loop, can be leveraged as a digital twin for end-to-end Open RAN System
* This paper shows the Colosseum architecture and
focused on how it enables a high-fidelity digital replica of
real-world RF environments, and also discusses how the digital twin integrates with real-world testbeds, and introduced several use cases where Colosseum digital twin capabilities have been used to advance algorithms, architecture, and testing of Open RAN systems
* Colosseum is constantly evolving to further improve its support for the design and evaluation of wireless systems

## Personal and Intuitive Indoor Navigation System based on Digital Twin

### Background:
Specifically, it is desirable that  navigation systems can provide the shortest path for those who  are in a hurry, barrier-free path for those are wheel chair users, or path with stairs for those who are eager to exercise. The  wide spread route navigation systems such as Google Map generally use GPS to acquire position  information. However, it is not possible to use navigation  systems inside the buildings where radio waves from  positioning satellites hardly reach. In buildings where  estimating a position by radio waves cannot be expected,  accurate position estimation by other means is demanded.

Therefore, in this paper, the author developed a system that acquires path information from a building to make navigation personal and create a digital twin with a graph structure where destinations or branch points are defined as nodes. Moreover, the author established an algorithm that automatically calculates the  shortest path using Dijkstra method after dynamically  changing the graph structure of a building. To estimate indoor  position, “static information” specific to a point such as  position fingerprint by Wi-Fi intensity and air pressure is combined with “dynamic information” related to the moving  state of a user detected by acceleration sensors, geomagnetic  sensors or timers implemented in a smartphone. Furthermore, the author established a multi-factor position estimation method that allows seamless and high-precision navigation in a multi-story and wide building by adding position correction with QR codes attached to nodes. We developed a user interface that Augmented Reality (AR) display can make the navigation intuitive. These applications are implemented as  smartphone  applications, which cooperate with a cloud server


### Proposed Solution: 
* Use case: When a user sets a destination and preferred movement  path such as recommend and barrier-free after starting a smartphone application, a path is calculated on the basis of the digital twin of a building on a cloud. As the user scans an adjacent QR code, it announces a direction displaying an arrow on AR. As the user approaches to the QR code at a next branch point, it notifies that the user is close to the QR code to be scanned. The user can reach a destination by repeating these steps. 
![image](https://hackmd.io/_uploads/rkP4Bq6hA.png)

* Method: There are few methods that are used to create this digital twin for indoor positioning.
    * Method to create digital twin: As graph theory can efficiently solve the shortest path problem, the focused on a graph structure that consists of  nodes and edges to create digital twins of buildings. Nodes correspond to main branch points or destinations and it is supposed that one QR code is attached to each node. An Edge represents that two nodes are linked. 

        The developed system can not only select a path according  to user’s preference but also navigate along with the selected path. Therefore, the system defines “static information” specific to a point which can make it possible to specify the point in buildings as properties of nodes and does “dynamic information” related to user’s movement which is needed for path calculation or navigation as properties of edges. Specifically, names of places, QR code IDs, the information of Wi-Fi that can be activated in the area, and air pressure are defined as node properties and distances (the number of steps, time of moving), types of paths (flatness, stairs, and elevators), and directions are as edge properties.
![image](https://hackmd.io/_uploads/B1wgUc63A.png)
    * Method to calculate personal paths: The graph structure of all paths in a building makes it easy to calculate the shortest path using Dijkstra algorithm. In this system, a user can choose a path according to his/her preference and there is a need to prevent the system from recalculating paths from a present point to a destination even when a user deviates from the given path. Therefore, the system is set to calculate all the shortest paths to a destination from all the nodes except for a destination after deleting edges besides types of path that a user chose on basis of path types applied to edges. 
    * Multi-factor position estimation method: The system estimates the point of QR code to be scanned next by combining position fingerprint and distances in horizontal movement. On the other hand, the author set a combination of position fingerprint and air pressure for estimating the next QR code in vertical movement. User’s position is corrected by scanning the QR codes. This multi-factor position estimation method can accurately estimate an indoor position by using both “static information” specific to a point such as QR code IDs, Wi-Fi information, and air pressure and “dynamic information” (distances) related to user’s movement.
![image](https://hackmd.io/_uploads/SJh6U9p2C.png)
    



### System Prototype
The author implemented a “building digital twin application” to be used by an administrator and an “indoor navigation application” by a user in an Android smartphone. 

* In the “building digital twin application”, functions to collect and register the point information of a QR codes attached to brunch points or destinations in buildings and the information between points are mounted. 
* The “indoor navigation application” has functions of operational UI for general users, acquiring and managing personal paths, estimating indoor positions and displaying moving directions in AR. 
* Functions to create building digital twins in the graph structure linking the “building digital twin application” and calculate personal paths cooperating with the “indoor navigation application” are packaged as a server application in a cloud server. Neo4j are used as a graph database. 
![image](https://hackmd.io/_uploads/HkuiPc6hC.png)
* To build the digital twin application, first the administrator generate a QR code and attach it to a point, then the administrator register some infromation to the attached QR code, which are “a name of a point” “a name of the building” “details” and “a floor”. When a “registration” button is pressed down after input, the application starts to keep acquiring Wi-Fi information of the point for three minutes once in four seconds. The Wi-Fi informations are acquired using WifiManager API and the information are "BSSID" and "intensity level (dBm)". These input or acquired data are sent to the cloud server by the POST method of HTTP and nodes are created in neo4j.
![image](https://hackmd.io/_uploads/BkmtAtRnR.png)


### Evaluation
* The author evaluated the accuracy of the position estimation of QR codes attached points between nodes and the functionality of the navigation
* To evaluate the accuracy of the position estimation of QR 
codes attached points between nodes, the author compared between using only position fingerprint by Wi-Fi and “dynamic information” related to user’s movement
* Position fingerprint by Wi-Fi works by comparing detected BSSIDs and registered BSSIDs at certain point. 
* The accuracy is calculated by determining if the application announced or displayed “a QR code is nearby” when it was within the radius of three meters from QR codes attached points
* The result is the accuracy was only 23 % with only Wi-Fi and 88 % with multi-factor
![image](https://hackmd.io/_uploads/rkBL75RnC.png)
* To evaluate the functionality of the navigation, the author asked seven students follow the navigation path for the evaluation experiment using the indoor navigation application and qualitatively evaluated the system with questionnaire survey.
* The result is all of the subjects could reach a destination and over 70% of them answered they could reach without any obstacle

### Conclusion:
In this paper, the author the author proposed the personal and intuitive indoor navigation system. This system is characterized by the algorithm that automatically calculates the shortest path using Dijkstra method after dynamically changing the graph structure of a building. To estimate a position during a user’s moving, the author established a multi-factor position estimation method by combining “dynamic information” which is the user movement with “static information” specific to a point. The results show that the system can select paths according to user’s preference and the accuracy of position estimation in the building is improved 3.8 times compared to a case where the position fingerprint by Wi-Fi intensity is applied. 

## Digital Twin Virtualization with Machine Learning for IoT and
J. Jagannath, K. Ramezanpour, and A. Jagannath, “Digital Twin Virtualization with Machine Learning for IOT and Beyond 5G Networks,” Proceedings of the 2022 ACM Workshop on Wireless Security and Machine Learning, May 2022. doi:10.1145/3522783.3529519 



### Background:
* Evolution of IoT networks has been a key enabler of modern techno logical developments including smart grid and city infrastructure, intelligent transportation, smart healthcare,etc. Massive number of IoT devices lead to a vast amount of data. Hence, intelligent technologies employing IoT networks face the major challenges of communication, processing and interpretation of big data.
* 5G mobile networks provide IoT devices with low latency and seamless connectivity for handling big data. AI and ML engines realize efficient algorithms for processing the data.
* Digital twin (DT) technology able to interpret the data, extract relevant information about the environment and thus enables the realization of the so-called hyper-automation
* Similar to SDN, the DT technology enables realization of optimal decision-making and control processes in a logically centralized process, possibly deployed on cloud platforms
* Another aspect of DT technology is virtualization of physical, objects and processes. DT models extend the virtualization of logic functions to any physical object or process. Hence, DT technologies provide a scalable solution for real-time monitoring and deployment of event detection and control processes for a massive volume of IoT devices.

### Capabilities:
* The classical role of DT is real-time monitoring of remote and distributed devices over an IoT network. It provides users with the current status and historic conditions and a data description for machine readable API
* Provide interoperability, defining a unified data description for heterogeneous IoT devices with a wide range of APIs and data formats
* Provides a platform for realizing policy exploration for intelligent control processes using Ran Intellignet Controller (RIC) from O-RAN on distributed systems


### Proposed Solution: 
![image](https://hackmd.io/_uploads/HyaWtr_hR.png)
* The architecture showed on the figure able to control services on a wide range of physical systems as compared with the networking function of 5G. The concept of service in the DT can also includethe networking service of 5G networks. In this perspective, a DT framework can model a 5G network for learning the optimal control policy, e.g. for the RIC functions in the O-RAN architecture 
* The deployment of control processes based on DT for 5G intelligent controller (RIC) can serve a twofold purpose.:
    *  First, the DT framework provides the RIC with simulation environments that can be used for Monte Carlo planning. This learning paradigm is not only beneficial in faster convergence of policy learning but also helps in predictive prevention and event detection. 
    *  Second, the DT based controller can be used for realizing off-policy reinforcement learning. The RIC implements the behavior policy that controls the (physical) 5G network. The DT deploys the target policy that is updated in the virtual space based on the observations from the (physical) network. The off-policy technique can help in converging to the optimal policy rather than a sub-optimal solution
* The functionality of each layer from the figure is as follow:
    *  The first layer in the proposed DT framework consists of DT models of individual physical entities within their local environment.
      ![image](https://hackmd.io/_uploads/rkHVcBu3C.png)
    *  As shown in figure, this layer directly communicates with the
physical space. The DT model of a physical entity consists of three main components: emulation model, predictive model, and synchronization engine. 
        * The emulation model represents the state and the behavior (interactions) of the entity in a given environment. The state can be a scalar value (e.g., battery percentage of an IoT device) or a multi-dimensional variable (e.g., a vector of geo-spatial state, data rate, security posture, computational and storage capacity).
        * The predictive model represents the dynamics of the local environment interacting with the entity. Given the environment dynamics, the future states and interactions of the physical entity can be predicted, thus the name predictive model. 
        * The synchronization engine (or training in the context of AI/Ml models) updates the models using measurements from the environment in real-time.
    * The second layer of the envisioned DT framework is model aggregation. This layer serves a twofold objective:
        *  First, it constructs the DT model of a physical system comprising of smaller devices or models. 
        * The second objective of this layer is aggregating
learning experiences of distributed DTs. Every DT learns a model
for the dynamics of its local environment. 
    * Aggregation of states (models) observed by many DTs can provide a wider visibility of the space. This is especially important for predictive and simulation capabilities of a DT framework.
    * At the third layer of the DT framework, networking and interlinking models are constructed. As discussed earlier, the physical space comprises of a set of distributed physical devices and processes under control (e.g., smart grid) and a data network infrastructure (e.g., 5G IoT). 
    * At this layer of the DT framework, the two physical systems are represented by two virtual models (e.g., interlinking model of smart grid and network model of 5G IoT). The interlinking model provides a high-level representation of the controlled system based on local observations of physical entities. Several control processes, corresponding to different service slices, might be associated with different interlinking models.
    * The fourth layer of the DT framework implements a simulation environment consisting of several virtual planes. Every plane models the physical space at different states. One virtual plane represents the current state of the physical space and can be used for
* The control and decision-making process in AI-enabled DT frameworks rely on live ML models of a physical space for optimal operation

### Conclusion:
* Digital twin (DT) is becoming an inevitable solution for implementation of complex control processes for distributed systems with observations over network
* Its capability in predictive modeling, based on real-time monitoring and data management, allows extensive test and verification of control policies before deployment on the physical space.

## Title

### Background:

### Proposed Solution: 

### Capabilities:

### Use Cases of Colosseum as Open Ran Digital Twin

### Experiments

### Conclusion: