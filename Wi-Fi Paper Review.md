# Paper Review about Wi-Fi Power Saving
Backround theory:
* [Wi-Fi(IEEE 802.11)](https://hackmd.io/@joshevan/HyZBgbrw1e)

List of Reviewed papers:
## A Comparative Analysis on benefits of Unscheduled Automatic Power Save Delivery Over Legacy Power Save Mode in IEEE 802.11 Wireless Networks
A. Sidam, P. Koutarapu, M. Methuku and S. Vuyyala, "A Comparative Analysis on Benefits of Unscheduled Automatic Power Save Delivery Over Legacy Power Save Mode in IEEE 802.11 Wireless Networks," 2022 9th International Conference on Computing for Sustainable Global Development (INDIACom), New Delhi, India, 2022, pp. 551-555, doi: 10.23919/INDIACom54597.2022.9763126. keywords: {Performance evaluation;Systematics;Wireless networks;Wires;Switches;Jitter;Traffic control;Unscheduled Automatic Power Save Delivery (U-APSD);Power Save Mode (PSM);Wi-Fi Multimedia (WMM);Quality of Service (QoS);Sleep;Doze;Access Point (AP);Station (STA);Target Wakeup Time (TWT)},

### Background:
Wi-Fi  is  a computer-based technology used to connect the internet  with smart devices in homes and organizational networks via a wireless interface to the internet. IEEE 802.11 uses various Wi-Fi frequency bands specific to 2.4 GHz and  5 GHz. It is very crucial for smart devices with limited storage space to have a better life and better performance, these devices should not drain out their energy when connected to the AP. 

IEEE 802.11 Standard added advanced features to MAC specialization which would extend battery life on wireless devices using a power-saving scheme (PSM). The basic idea  of PSM is to save energy when the device is not in usage. There is a lot tof work has been accomplished in modifying the Legacy PSM to lower energy consumption further. Previous work showed that there is a considerable amount of energy saved at the cost of long jitters. The Legacy PSM leaps over the same output for all kinds of traffic categories. In addition, a Legacy PSM is better suited for the Background and Best Effort traffic but not for real-time audio and video traffic. This paper explores how IEEE 802.11 amendments of Unscheduled Automatic Power Save Delivery (U-APSD) is working fully with a low jitter for real-time traffic as compared with the legacy PSM.

### Methodology:
This section focuses on how Legacy Power Save  mode (PSM) and an Unscheduled Power Save mode (U-APSD) method works in the wireless LANs. According to IEEE 802.11, every AP transmits Beacons at regular intervals to show its presence, to make all authenticated 
stations/clients in the Basic Service Area (BSA) connect to 
it. 
* **A.Legacy Power Save Mode**
In IEEE 802.11 legacy PSM, the STA will be either in awake or a power save (PS) mode. In the awake state, STA is always active to send and receive data. When the STA is awake and there is no data to neither send or receive, the radio sleeps for unlimited time and is constantly powered. Hence it can send and receive data continuously. The Beacon frame contains STA’s next awake time and is equal to a number of BI’s and STA can possibly be in a doze mode. Figure below shows state between STA, either sleep or awake.
![image](https://hackmd.io/_uploads/HJQKXR1d1x.png)
The STA always intimates using Qos NULL Frame to the AP before transiting its state and waits for the successful ACK. The Client alters between Active to PS Modes and the energy consumed is negligible. The client switches between transition modes successfully by notifying the AP with a frame exchange. A Null frame is commonly used by the client. Figure below shows a Qos NULL Frame PM=1 indicates client active and Qos NULL Frame PM=0 indicates the client is in PS mode.
![image](https://hackmd.io/_uploads/SJr67Ckd1l.png)
The Access Point uses Delivery Traffic Indication Map (DTIM) for Broadcast Traffic and Traffic Indication Map (TIM) for unicast Traffic at every Beacon frame to buffer packets across it. When the STA switches to PS Mode, AP buffers all incoming packets and waits till the destined STA is awake. When the STA is in PS mode it can wake up indefinitely if it has any data to send. Meanwhile, if STA  notifies data buffered at AP  it sends PM-Poll to AP.  PM Poll performs selection among  all STAs which are active so that data can be buffered at AP. 
![image](https://hackmd.io/_uploads/BJyOVCyukl.png)
One main concern with this protocol is that even though there are no buffered packets at AP the STA activates for every Beacon time. Hence, energy is consumed when the client switches from active to PSM. This energy consumed totally relies on and compares with energy consumed in the number of packets received. Hence, the frequency of STA switching from active to PS modes must be decreased gradually for reduced power consumption. In precise Legacy, PSM is the best suitable for Background and Best Effort where  long  Jitter is not a concern. 

* **B.Unscheduled –Automatic Power save Delivery (U-APSD)**
IEEE 802.11 amendments advanced with Unscheduled Automatic Power Save Delivery (U-APSD) which are best suited for real-time (Audio and Video) traffic. The U-APSD mechanism requires data that are available at the MAC layer. The work totally depends on the conjecture that limits in a delay are either retrieved from the upper layer or present at the MAC layer. These time delays are common for all types of traffic connected on the same Access Categories. 
Figure below shows the Unscheduled Automatic power save Delivery (U-APSD), where an AP sends buffered frames independently to enable AC’s that expects real-time data delivery. As Legacy PSM uses more bits iteratively even U-APSD uses a More bit =1 to receive the data frames. When it reaches 0 there is no more data buffered at an AP. The STA is awake till the Unscheduled AC is ended by the AP and by enabling EOSP bit set to 1, a final QOS frame is sent to intended STA. U-APSD offers good Qos of AC’s because it triggers at random time slots. It triggers on the traffic type instead of Beacon intervals (BI). U-APSD also reduces the burden of retrieving the frames buffered at the AP. This might help VOIP applications where Qos NULL frames are not required, and IEEE 802.11 PS-POLL overhead is considerably reduced. 
![image](https://hackmd.io/_uploads/Bk8CH0J_kx.png)

### Experiments
In this section, this paper analytically model the power save mode in IEEE 802.11 infrastructure network. This paper obtain the average value of jitter at different time intervals as performance measures using this model. To understand better. this model works on the presumption that every client has its own proprietary rules to switch between active mode to power save mode and IEEE 802.11 defines the client to be in three modes. 

* Constantly Awake Mode (CAM): Most of the time the station is active. This mode provides the highest throughput but consumes more power. 
* Fast Power Save Polling (Fast PSP): Depending on the traffic load the station switches between active and Power Save mode. The client stays in PS mode When the traffic is idle or very low. 
* Maximum Power Save Polling (Max PSP): Most of the time the radio is in Power Save. This mode saves the most power but also provides the lowest throughput. In this model, use Wireshark packet capture, and the station is in CAM mode scanning its neighboring APs for every 10 seconds. 

#### Testbed used for evaluation 
The testbed comprised of small Wireless LAN with some private enterprise products. A laptop is a server that receives or sends data and collects traffic analysis information from clients. It is connected to a wireless router over wired connection and Device under Test (DUT) is a wireless STA connected wireless with AP. Wired Station Streams are sent to a wireless station. Packet flows are generated with different Access Categories (AC) using PING Utility with the –v option. With a computer-based Wireshark network analyzer, packets are captured in Legacy PS Mode. When the AP is awake constantly (CAM) the client scans its neighbor APs for every 10ms. The topology is shown in figure below
![image](https://hackmd.io/_uploads/rJKgO0J_Je.png)

In order to switch from active to PS Mode, the client sends a Qos NULL data frame with PM=1 and notifies all neighboring APs using a Probe Request Frame. Hence, the AP starts buffering the packets destined to STA using respective AID notifying TIM Bitmap of the Beacon. Later when the client is awake the client checks for any buffered data. The STA may go back to sleep after some Beacon Intervals with the possibility of losing data. The client goes back from PS Mode to Active state enabling PM = 0. In the test bed, the STA is assigned with a 20ms Listen Interval. Hence the Client has to activate for every 20ms LI to find out the buffered data. The AP frees the buffered data for every 20ms LI if the client does not receive it.

For U-APSD using the trigger frame, there is a control for AP to find out how often the client is awake and can receive data. When there is a trigger Frame from STA it awakes every 20ms and notifies the available Voice AC’s. Now the AP buffers the data until EOSP =1 to notify end of delivery. Hence,the STA goes back to sleep. After 20ms it wakes and again sends the voice data which is still in PS mode. If there is no buffered data across the AP it sends QoS Null Frame with PM=1 to notify the end of delivering data. 

The results obtained for 10 iterations on wireless STA got an average of 105ms with Legacy PSM Whereas with U-APSD got an average of 21ms. 
![image](https://hackmd.io/_uploads/HJOh_01_1l.png)

### Conclusion:
A Systematic approach is performed to minimize a low jitter and latency with a Legacy PS mode and U-APSD. This paper determined the power consumed by the wireless devices and its impact when it switch between active to sleep mode and also how the quality of a voice over an IP is affected with this transition. This focused on the different packet flows with a different traffic pattern and determined the experimental results with a jitter of 105ms Hence Legacy PS Mode is said to be well suited for the Background and Best Effort where Jitter and a latency is not a concern. With U-APSD there are low jitter values which improved the quality of voice traffic. 

For future work, the Target Wakeup Time (TWT) in  IEEE  802.11ax will be analyzed. A TWT is said to use different Qos by scheduling various TWT sessions allowing transmission on traffic with priority data (Video/Audio). An efficient sleep time is considered in the scheduling technique and PS mode is  analyzed  for  better life of nodes and  more  importantly  on  the  power  storage. In Addition, the experiment is preferred to work in real-time environments for wireless networks. 


## Optimizing Power Consumption for Business Networks through Cooperative Communication in Mixed Wireless Environments

### Background:
The increasing usage on mixed wireless environments, integrating cellular networks, Wi-Fi, and other technologies, has resulted in increasing energy consumption within business networks. This causes significant environmental and financial challenges. Hence, the concept of cooperative communication presents a promising solution for addressing the energy efficiency dilemma in mixed wireless environments.

Cooperative communication refers to a network design philosophy where devices work together to facilitate communication, rather than operating in isolation. This approach enables devices to share resources and relay information, thereby reducing the power required for transmission and improving overall network efficiency.


### Proposed Solution: 
This paper proposes a comprehensive framework to optimize power consumption in business networks. The approach is the integration of advanced cooperative communication techniques, such as relay-assisted transmission and network coding, alongside dynamic resource allocation algorithms. The approach aims to reduce power consumption across mixed wireless environments by integrating spatial diversity and enabling resource-efficient data transmission, without sacrificing service quality, thereby contributing to more sustainable and cost-effective network operations.

The detail of the proposed framework:
* **A. Cooperative Communication Techniques**
    * Relay-Assisted Transmission: Uses intermediate nodes to forward data, reducing the power required for long-distance transmissions.
    * Network Coding: Combines multiple data streams into a single transmission, decreasing the total number of transmissions.
* **B. Dynamic Resource Allocation**
    * Allocates resources like bandwidth and power in real-time based on network conditions and energy efficiency metrics.
    * The optimization problem for dynamic resource allocation can be formulated as minimizing the total energy consumption subject to network performance constraints (such as throughput and latency)
![image](https://hackmd.io/_uploads/HJ-wpMW_yx.png)
* **C. Network Optimization Algorithms**
    * The network optimization algorithm determines the most energy-efficient routes, modes of communication, and scheduling protocols by considering various factors, including the energy profiles of devices, current network traffic, and the potential energy savings from using different transmission techniques. 
    * The efficiency of network coding can be modeled as the ratio of the number of transmissions required without network coding to the number required with network coding. Higher efficiency means higher power saving as fewer transmissions mean less energy consumed.


### Experiments
Simulations were conducted in mixed wireless environments to evaluate the framework. Key metrics analyzed are energy efficiency, which is the ratio of the data transmitted and the energy consumed, throughput, throughput, and latency. The results from the simulation studies showed significant reducing power consumption across business networks.

![image](https://hackmd.io/_uploads/BkiH0fbOJx.png)
The result shows reduction in average power consumption with the proposed framework, demonstrating the benefits the proposed framework. While there is a slight decrease in data throughput and a minor increase in latency, these trade-offs are minimal compared to the gains in energy efficiency.

### Conclusion:
The study introduces a framework that enhances the energy efficiency of business networks in mixed wireless environments. By integrating cooperative communication techniques with dynamic resource allocation and optimization algorithms, the framework achieves significant reductions in power consumption without compromising performance metrics. This research provides a foundation for the optimization of mixed wireless networks, also greener, cost-effective, and sustainable telecommunications practices.




## Deep Learning-Based Radio Estimation Using a Semi-Automatically Created Indoor Building Information

### Background:
The widespread adoption of wireless communication in fields such as transportation, construction, and healthcare has led to a need for optimized wireless network construction. The coexistence of various wireless systems, such as, Wi-Fi, Bluetooth, 5G, poses challenges in determining the optimal placement of access points (APs) and adapting to changes in building layouts. Pinpointing the appropriate location for installing APs can be challenging due to various factors such as building layout, terminal mobility, and obstructions, which can impact the quality of wireless connections. Traditional methods of wireless network deployment are time-consuming and costly due to their reliance on expert evaluations and iterative trial-and-error processes. This paper address this challenge by leveraging deep learning method.

### Proposed Solution: 
This paper presents two main contributions: 
* A semi-automatically created database that describes indoor building information including the indoor building constructed by the walls, ceiling, and floor, as well as the objects (e.g.,chairs, sofas, tables, others.) located within the building
* A wireless estimation method based on deep learning using the aforementioned database. The deep learning method, called RadioResUNet, is  designed to predict the RSS of a 2.4GHz Wi-Fi system in complex indoor environments, which may have multiple walls and obstacles. This is done by using two input parameters: the building layout and the position of the AP’s antenna.

### Methodology:
 This section presents two main functions: a semiautomatically created database that describes indoor building information and a wireless estimation method based on deep learning using the aforementioned database

* **A. Creating Database for Indoor Building Information**
    * Point Cloud:  A point cloud is a collection of data points in a 3-dimensional coordinate system defined by their x, y, and z coordinates, representing the spatial location of objects or surfaces captured by sensors
    * Plane Segmentation:  Within buildings, there are various objects with different shapes, while ceilings, walls, and floors are examples of specific objects with planar surfaces. Plane segmentation involves extracting planes from the point cloud. The RANdom SAmple Consensus (RANSAC) algorithm is commonly used for this purpose, as it effectively identifies planes in point clouds
    * Object Detection: This paper employ the ”Towards Real-Time Indoor 3D Object Detection (TR3D)” method which enables fast and fully-convolutional 3D object detection from point clouds
    * Building Information Database: The information of objects detected through plane segmentation and object detection by TR3D is automatically registered in a database (DB), while any missed information is manually added to the DB
    *  3D Modeling: To ensure the accuracy of the building information stored in the DB, this paper generate a graphical 3D model using the IFC data format

* **B. Radio Estimation by Deep Learning**
    * Deep Learning Network: This paper use RadioResUNet, a convolutional neural network, which trained on datasets of indoor layouts, AP positions, and ray-traced radio-maps to predict RSS. To train and validate RadioResUNet, we use radio-maps created by ray-tracing with the following parameters: a frequency of 2.4 GHz, a transmitter antenna height of 2.5 m, a transmit power of 200 mW, and isotropic antennas with 0 dBi for both the transmitter and receiver.
    * Input Indoor Layout: RadioResUNet requires two types of input data: the indoor layout and the position of AP within the building. To use the 3D indoor layout from the DB in RadioResUNet, it is necessary to convert the layout into a 2D format.
    * Input Antenna Position: The strength of the radio signal is significantly influenced by the distance between the transmitter and the receiver. RadioResUNet predicts the RSS based on the AP’s antenna position relative to the indoor layout.

Image below is the processing flow and example for deep learning-based radio estimation with semi-automatically created indoor building information.
![image](https://hackmd.io/_uploads/B1Bki4-_1x.png)


### Experiments
The method was validated in an office setting:

* A 3D model of the office, with dimensions of 12 m 12 m 2.7 m, was generated from the database and used to train RadioResUNet.For these measurements, a Wi-Fi system with a frequency of 2.444 GHz, a transmit power of 200 mW, and  omni-directional antennas with 0 dBi gain for both the AP and terminal is used.
* RSS predictions were compared against practical measurements taken using a robot equipped with a Wi-Fi receiver. The average deviation between predictions and measurements was approximately 3 dB.
* A modified layout was tested by updating the database, demonstrating the model's adaptability to layout changes with similar accuracy levels, around 3dB.

Image below is the An office room and the 3D model configured by building information in DB
![image](https://hackmd.io/_uploads/BJgb6VZO1x.png)

Below are results of radio prediction and practical measurement for the office room, before and after modified
![image](https://hackmd.io/_uploads/H1kUaVbOJe.png)

![image](https://hackmd.io/_uploads/r1KLT4ZuJx.png)


### Conclusion:
This paper proposed a deep learning-based radio estimation approach that utilized semi-automatically created indoor building information. The proposed framework enables efficient, accurate, and cost-effective RSS estimation in indoor environments. By leveraging deep learning and semi-automatically created building information databases, the system provides wireless predictions for new or updated layouts without requiring extensive manual adjustments. This approach simplify wireless network design and reconfiguration, saving time and resources while ensuring optimal connectivity.




## Towards an energy-efficient Wi-Fi: An experimental study on recent standards power consumption
François Lemercier, Anne-Cécile Orgerie. Towards an energy-efficient Wi-Fi: An experimental study on recent standards power consumption. WCNC 2025 - IEEE Wireless Communications and Networking Conference, Mar 2025, Milan, Italy. pp.1-6. ffhal-04928381f

### Background:
Conducting power consumption measurement experiments on Wi-Fi devices represent several challenges due to the complex and dynamic nature of Wi-Fi communications. Multiple factors impact significantly the power usage of the WiFi transmitter such as the strength of the signal, the traffic patterns, the environmental conditions (interference or network congestion). Furthermore, advanced features such as MIMO,
power saving mechanisms, adaptive transmission power, or
even beam-forming can complicate the measurement by introducing variable consumption patterns.

 In addition, there is no standardized measurement process to capture the microsecondlevel fluctuations of Wi-Fi transmitters. Wi-Fi devices interact with other system components such as CPU and memory leading to inter-dependencies that make measurement difficult to isolate. Moreover, the heterogeneity of Wi-Fi standards and implementations add more complexity, as different devices may behave each in their specific way. Consequently, conducting an accurate and precise power consumption measurement experiment on Wi-Fi devices requires careful control of external factors and the use of specialized tools able to capture detailed power profiles over various states of operation.


### Proposed Solution: 
In this paper, the author conduct an experimental evaluation of the power consumption of a selection of USB Wi-Fi devices, focusing on the latest standards such as IEEE 802.11ax and IEEE 802.11ac. Using USB devices allows to isolate Wi-Fi behavior and to provide accurate measurements in the different MAC states: idle, transmitting, receiving, and sleeping. Such power measurement values remain scarce, although they are required for any simulation-based evaluation as input parameters, for instance in the well-know ns-3 simulator.

### Methodology:
1. Overview: 

This experimentation protocol is designed to measure the energy consumption of Wi-Fi devices across different operating states: transmission (Tx), reception (Rx), idle, sensing when the channel is busy (CCA busy) and sleep. The testbed consists of modern Wi-Fi chipset (802.11ac and 802.11ax), a power measurement tool with 100k sample per second resolution, and a controlled network environment to minimize external interference. The protocol involves systematic measurement of each device listed in table below

![alt text](assets/images/Power%20Consumption/Parameters.png)


2. Experimental Setup:

The setup of the test bench for the experiment:
* An AP, a STA and an Ethernet client
* The STA is the only Wi-Fi device associated to the AP
* Six different models of USB Wi-Fi cards are used, the list can be seen on table below
* The AP is a IEEE 802.11ax Tp-Link Archer AX50
* The STAs are connected to a Dell Latitude laptop (Intel Core i7 2.80 GHz CPU, 32 GB of RAM) running Windows 10, using iperf benchmark
* The Ethernet client is connected using an USB-C 1000 Mbps Ethernet adapter on an Apple MacBook Pro (Intel core i9 2.4 GHz, 16 GB of RAM) running iperf application on Mac OS 14.5
* A Nordic Semi Power profiler II power meter is interconnected between the STA and the Windows PC on the power supply line of an USB extension cable. 
* The AP is configured to deliver its maximum transmission power 
* All the USB WiFi cards are configured to use the IEEE 802.11ac or IEEE 802.11ax, and maximum transmission power
* The AP broadcasts its SSID on channel 5220 MHz and a bandwidth of 80 MHz, MIMO is enabled
* Each STA device is configured to operate at its maximum speed, with a fixed channel width 

![alt text](assets/images/Power%20Consumption/List%20of%20devices.png)

3. Measurement Methodology
The methodology of the measurement:
* The measurements are carried out by sending and receiving large data packets under different configurations.
* The power consumption is measured at the STA side of the test bench during various phases: wake-up, data transmission, reception, sleep and idle periods between transmissions
* The current consumption data are collected with the Nordic Semi Power profiler Kit II with a sampling period of 10 µs and a granularity of 100nA
* AP and STA are deployed in a indoor environment, with a short distance of 1 meter between each other to reach the maximum throughput available
* There is no power measurement on the AP device, this experimentation is focused on the STA device

### Experiments
Below are the experimental results obtained for each of the considered MAC states.
1. Idle power consumption analysis

The idle state is the state when the STA, being associated with the AP, neither sends nor receives traffic. Figure below shows the mean value of the current consumption measured across multiple tests for each device. The whiskers illustrate the standard deviation of the measurements, showing a low variability of the idle current consumption, except for the Netgear A8000 device having a lower average idle current consumption with a high variability. Apart from the Netgear device, all other STA are roughly within the same order of magnitude, with the difference are between USB3 and USB2 links
![alt text](assets/images/Power%20Consumption/idle%20curent%20consumption.png)
 
2. Transmission power consumption analysis

The author first measure the maximum instantaneous value of current drawn by the device during a transmission phase for each STA device, at the scale of a packet. Secondly, the author measure the power consumption of each STA device during a transmission phase of 10 seconds depending on the target bandwidth at the client side.

The result of the first experiment are shown in table below
![alt text](assets/images/Power%20Consumption/Instantaneous%20result.png) 

The results of the second experiment are shown in figure below
* TCP Traffic

![alt text](assets/images/Power%20Consumption/TCP%20Traffic%20Tx.png)
* UDP Traffic

![alt text](assets/images/Power%20Consumption/UDP%20Traffic%20Tx.png)

Both Figures show that increasing the target bandwidth has impact on the current consumption of the device, except for the Asus device. This may be explained by the device itself, where the chipset used (RTL8852AU IEEE
802.11ax) is coupled to a USB2 interface which is not fast enough to saturate the maximum data-rate reachable with this Wi-Fi chipset.

Also, the current consumption is lower for an UDP traffic when the traffic is slow but reaching the highest data rates, having a faster throughput, the current drawn at high speed is higher compared to a TCP traffic.

3. Reception power consumption analysis

To characterize the reception phase of the STA device, the same experiment as the transmission section is conducted, but the iperf server is located on the STA laptop and the client sending data is located on the Ethernet laptop. First the maximum instantaneous value of current drawn by the device during a reception phase for each STA device, at the scale of a packet is measured. Secondly, the power consumption of each STA device during a reception phase of 10 seconds depending on the target bandwidth at the client side are measured. 

The results of the first reception experiment are shown in Table above in the rx curent. 

The results of the second experiment are shown in Figure below.
* TCP Traffic

![alt text](assets/images/Power%20Consumption/TCP%20Traffic%20Rx.png)

* UDP Traffic

![alt text](assets/images/Power%20Consumption/UDP%20Traffic%20Rx.png)

Both Figures show that each measured STA has a similar behavior, only differentiated by the idle current consumption as an offset. We can observe a slightly higher increase of current consumption when using TCP compared to UDP on each STA.

4. Using the Obtained Experimental Values Within simulation Tools

Simulator frameworks, such as ns-3, can take advantage of the current values obtained in the previous section.

* NS-3 energy model: The popular discrete event network simulator ns-3 propose
a Wi-Fi energy model that provide a detailed framework to estimate the power consumption of Wi-Fi devices by capturing their behavior across different operational states, such as transmission (Tx), reception (Rx), idle, sleep and CCA busy. This energy model is integrated in the simulator Wi-Fi protocol stack, which includes the support of various IEEE 802.11 standards from 802.11a to 802.11ax and allows to take into account the factors of influence of each standards specificity on the power consumption. It also accounts for power-saving mechanisms such as PSM and TWT.

    Despite its versatility, the accuracy of the ns-3 Wi-Fi energy model highly depends on precise calibration with real-world power measurements. Furthermore, the evolution of Wi-Fi technologies require updates to the energy values in order to account for the specificity of each standard. Few studies have considered updating the default values and behavior to modern Wi-Fi devices, particularly those implementing 802.11ac and 802.11ax. This work tries to provide new values and recommendation to improve the accuracy and the realism of future simulations of Wi-Fi architectures.

* Comparing ns-3 current instantiation with our own: The author compare results obtained with the default ns-3 values against results obtained with the ns-3 models instantiated. This paper select the values measured on the most stable STA device (having the smallest standard deviation on all measured current values), the Tp-Link TX20H and then create a simple Wi-Fi scenario consisting in a unique STA associated to an AP, with the same parameters as described in the test-bed.

    Figures below show a comparison of the measured current values for the second experiment for the Tp-Link TX-20H connected in USB3 (TPL3), with the default current values of the ns-3 Wi-Fi energy model (ns-3) and the ns-3 energy model updated with the current values (Facto). Focusing on the transmission, no matter the transport protocol used, the result show that the default ns-3 model can be close to the measured values only for medium data rates, but the model updated with the values offer a similar behavior despite having a slight offset.
    - Tx TCP ns-3 Comparison
  
    ![alt text](assets/images/Power%20Consumption/TCP%20ns-3%20comparison%20Tx.png)

    - TX UDP ns-3 Comparison

    ![alt text](assets/images/Power%20Consumption/UDP%20ns-3%20comparison%20Tx.png)

    - Rx TCP ns-3 Comparison
  
    ![alt text](assets/images/Power%20Consumption/TCP%20ns-3%20comparison%20Rx.png)

    - Rx UDP ns-3 Comparison

    ![alt text](assets/images/Power%20Consumption/UDP%20ns-3%20comparison%20Rx.png)

     Results on the reception show a better accuracy of the ns-3 model with higher data-rates. The ns-3 model updated with the current values shows a slightly more comparable behavior with our measurements, but shows differences with medium data rates


### Conclusion:
This paper introduces a comprehensive experimentation protocol for measuring the energy consumption of modern WiFi devices. The results demonstrate the complexity of energy  usage in Wi-Fi networks, especially when considering devices with advanced features like MIMO, channel bonding, and adaptive modulation.

The findings suggest that a careful selection of current values in ns-3 energy model, especially the idle and transmission values, can significantly precise the power consumption and increase the accuracy of energy efficiency improvement studies.

Future work will focus on extending these experiments to more complex network environments and newer Wi-Fi standards, such as 802.11be and also to explore the impact of dynamic network conditions, such as interference and mobility, on energy consumption, as well as a detailed analysis on the current consumption during the wake-up phase of an STA device.

## AI/ML-based Load Prediction in IEEE 802.11 Enterprise Networks

### Background:
Several studies have shown remarkable performance in several enterprise Wi-Fi deployments by leveraging AI/ML-based traffic prediction solutions. However, the practical adoption of AI/ML solutions still raises concerns and leaves many questions unresolved. The complex nature of events occurring in networks at different time scales (e.g., from ms-order variations to yearly-seasonal patterns) poses a trade-off between the achievable performance by AI/ML methods and their complexity, which entails costs in terms of computation and memory needs, energy, and time.

### Proposed Solution: 
This paper talk about the gap between the performance of relevant state-of-the-art AI/ML models and the cost and feasibility of training and maintaining them in practice. More specifically, this paper focus on traffic prediction for enterprise Wi-Fi utilizing an open-source dataset, which includes measurements from thousands Access Points (APs) in a wide campus network. The challenge in this work is the resource trade-off in terms of data collection, training and re-training needs, computational complexity, and energy when designing ML models to be deployed in real environments.

### Methodology:
  1. Time series forecasting
Let X<sub>T−L:T</sub> = {X<sub>T−L</sub>, ..., X<sub>T</sub> } be a series of features collected across L consecutive lookback points and up to time step T, where each measurement is a feature vector x<sub>t</sub> ∈ R<sup>M</sup> containing M features. The goal of the time series forecasting problem is to predict the values of a subset of selected features N ⊆ M in the future next S time steps. For that, supervised learning is used, where available data is used to fit the weights W of a forecasting function fW. In this work, different models are used as forecasting function . The optimization of the models and is driven by the minimization of a loss function, which compares each prediction with its ground truth.

2. Evaluation metrics
The performance of a model can be calculated as 

A(fw) = $\sum_{p∈P} ϵf$ (Y<sub>p</sub>, Ŷ<sub>p</sub>),

where ϵf is an error function, and Ŷ and Y are theconsidered predictions and actual values, respectively. In this work, the Mean Absolute Percentage Error (MAPE) is used as the main model accuracy metric, which is computed as

MAPE = 100 × $\frac{1}{p}$ $\sum_{p=1} ^{P}$  $\frac{|Ŷp - Yp|}{|Yp|}$

MAPE provides a good
intuition about the suitability of different models for assisting load-prediction-driven applications (e.g., switching off APs with a forecasted load below 10%)

3. Dataset

Dataset used are the open-source dataset, which contains 25 074 733 association records (from a total of 55 809 users) extracted from 7404 Wi-Fi APs distributed in a campus area, during 49 days in 2019. 

The data contains features such as the user Medium Access Control (MAC) address, the ID of the AP to which the user is associated, and the number of Bytes transferred per session. The selected dataset, while depicting the network activity in a campus network, provides good insights for enterprise use cases, where Wi-Fi is mostly deployed for non-business critical applications (e.g., office tools, online meetings).

4. ML models
Various ML models for addressing the load prediction problem:
* ARIMA: ARIMA(p, q, d) is a statistical model used to predict the evolution of time series through autoregression (p), integration (q), and moving average (d). In this work, ARIMA is used as a non-ML baseline model. Since ARIMA is a univariate statistical model (it cannot be trained like the rest of ML models and then used to generate predictions on new data), an instance of ARIMA is generated for each AP under evaluation and apply it directly to the evaluation data. For every set of predictions, an ARIMA model is fitted with data from the previous 24 hours and apply it using the parameters. This approach is costly and, thus unsuitable to be applied in real-time
* LSTM: A type of RNN designed to address longrange dependencies in sequential data thanks to the usage of LSTM cells, which allow capturing temporal dependencies across time series data. In this work, the time series of network data are passed through a few LSTM layers before a predictive output is generated by a feed-forward fully-connected layer.
* CNN: A class of deep NN that automatically learns hierarchical patterns (e.g., edges and shapes from an image) and features from the data by utilizing convolutional layers and other data transformation techniques like down-sampling. In this paper, the time series vectors of network information features are processed as if they were images by several 2D convolutional layers

### Experiments
In this section, the models explained before are evaluated when applied to the load prediction problem in enterprise Wi-Fi. For the evaluation of the models, the first 80 % of the measurements of a specific AP used as training and validation data and the remaining 20 % as test data

1. Data collection requirements

    In this case, the design and size of ML models are strongly influenced by the length of the observation window and the granularity of the measurements. Figure below shows the MAPE achieved at S ∈ {10 min, 30 min, 60 min} steps by each model when using G ∈ {10 min, 2 min, 1 min} granularity values

    ![alt text](assets/images/Load%20Prediction/Granularity.png)

    From the figure, it can be seen that the granularity of the measurements has a significant impact on the models’ performance and poses a trade-off between accuracy and data collection. In particular, ARIMA with G = 10 min leads to prediction errors around 25% when S = 10 min, increasing to 92% for farther away predictions (S = 60 min). For LSTM and CNN, in contrast, the prediction error with G = 10 min remains stable, and mostly below 30%, at the different values of S. 

    It is very important to find a good compromise between capturing fine-grained events and keeping the complexity low, and this is something properly captured by G = 2 min for the dataset in use. Based on these observations, the granularity of data acquisition to 2 min will be used for the remainder of the paper

2. Training needs and generalization capabilities

    To assess the model generalization capabilities, the author evaluate the different models into different sets of APs with sizes Ktest ∈ {4, 16, 32} and we differentiate between onpremises (on-prem) and off-premises (off-prem) training approaches. On-prem uses the training data from thesame set of test APs, which is useful to generate specialized models ,but it requires significant time for collecting data. As for off-prem training, models are trained using data from a different set of APs, thus becoming less specialized but allowing for immediate deployment of ready-to-use models.

    ![alt text](assets/images/Load%20Prediction/Test%20sets.png)

    Figure above shows the MAPE achieved through N = 10 experiments and for G = 2 min. By comparing the performance of the on-prem and off-prem versions of CNN and LSTM, we observe a clear advantage when training models on-prem. This effect is intensified in small deployments (Ktest = 4), where data heterogeneity is lower, thus allowing for better specialization of the model. As a downside, on-prem training requires doing measurements on-site (e.g., during weeks), which is costly and not always feasible. While on one side off-prem models would speed up the deployment of ML solutions at new sites, on the other side it is not accurate and considering a short re-training on-premises may be required to decrease their prediction errors. Based on these observations, K test = 4 and on-prem versions will be used to better focus on the capability and performance of the pure ML models

3. Deployment feasibility and energy consumption
   To assess the feasibility and cost of adopting the proposed ML-based solutions in real deployments, the author focus on the energy consumption, the training and inference times, and the memory footprint of the models. The author consider that model (re)training is done every two weeks from the data of Ktrain = 4 APs, while model inference is performed every time a new measurement arrives.

    This analysis is conducted in two different computation environments:
    *  top-range ML specialized equipment using an A5000 24 GB NVIDIA GPU
    *  consumer-level equipment using an AMD Ryzen Threadripper 3970X Processor of ×32 cores 
      
    ![alt text](assets/images/Load%20Prediction/Computation%20time.png)   

    As shown, CNN and LSTM lead to similar values:
    * requiring training times of a few seconds and inference times in the order of milliseconds.
    *  the memory needed is small
    *  the energy consumed by either applying (inference) and training the models has resulted in general very low
    
    Overall, this confirms how reasonably good predictions can be obtained even with cost-effective models.

4. Model Optimization

     ML model optimization is of utmost importance for the sake of minimizing the operative costs of AI/ML-based applications. Among several model optimization techniques, ML model compression (e.g., pruning, quantization) stands as one of the most appealing methods to save computational time, bandwidth, and energy without sacrificing performance excessively. Applying post-training static quantization to the ML models able to reduce size thus speeding up the inference time while preserving the same accuracy levels.

### Conclusion:
A prominent use case of AI/ML in communication is traffic prediction, which unlocks advanced network capabilities for self-troubleshooting or proactively saving energy. This paper explored the potential of AI/ML-based traffic prediction in enterprise Wi-Fi networks, linking performance with feasibility. The result showed that finding a suitable measurement granularity is key to keeping mean prediction errors below 25%, also using on-prem trained models for use cases requiring far-future predictions. In terms of cost, the real-time usage of all the studied ML models leads to modest energy consumption values when deployed in commonly available hardware equipment.

## Title

### Background:


### Proposed Solution: 

### Methodology:

### Experiments

### Conclusion: