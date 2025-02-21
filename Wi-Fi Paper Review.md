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

## A spatio-temporal prediction methodology based on deep learning and real Wi-Fi measurements
Shaabanzadeh, Seyedeh Soheila, and Juan Sánchez-González. "A spatio-temporal prediction methodology based on deep learning and real Wi-Fi measurements." Computer Networks (2024): 110569.


### Background:
The recent development of (Big) Data monitoring and analytics technologies is one of the main pillars in cellular/Wi-Fi networks to deal with the new multimedia services that have very strict requirements in terms of reliability, latency, bit error rate, etc. In particular, the capacity to collect information about the users and the network by deploying monitoring tools, and the capacity to extract knowledge of the collected data by means of Artificial Intelligence/Machine Learning (AI/ML) technologies can help the network to be smarter, more intelligent, self-aware, cost-efficient, and self-optimized.

The future network traffic prediction can be useful for supporting different decision-making processes over the network related to network reconfiguration and optimization, such as proactive resource allocation, prevention of congestion/overload situations or activation of load balancing processes to distribute network traffic among multiple cells/APs.

### Proposed Solution: 
This paper addresses spatio-temporal prediction of a specific Wi-Fi metric by developing an adaptive and context-aware prediction framework. This framework dynamically adjusts to spatial dependencies among APs, enhancing the accuracy and reliability of traffic predictions. This paper compared a wide range of techniques including more recent prediction techniques, alongside single and hybrid NN techniques in terms of prediction accuracy and computational time to achieve more comprehensive result. 

The proposed methodology is evaluated in a real Wi-Fi network with measurements collected from a large number of APs (i.e. 100 APs) over three months. This addresses the challenge of scalability in designing prediction systems for Wi-Fi networks, ensuring that the methodology can effectively handle larger network environments without compromising performance.

### Methodology:
The architecture of the methodology can be seen on figure below
![alt text](assets/images/spatio-temporal%20prediction/architecture.png)

* Data collection:
  * Network measurements collected at the APs are sent to the Wireless LAN Controller (WLC) and stored in a centralized database 
  * An offline training is ran periodically in order to extract knowledge from the collected data and to keep the model updated
  * The proposed methodology aims to predict future values of this specific metric in a given AP by using the last several collected measurements
* Data preparation: 
  * Automatically determining missing data in some time periods using backlifting, which is filling missing data with the data of previous time period
  * Normalized the input data so that all values are within the range between 0 and 1.
  * Calculates the correlation between each AP and all its neighbours. AP neighbours are determined by means of the Neighbour Discovery Protocol (NDP). If the AP has highly correlated neighbors, spatio-temporal prediction is done based on the previous measurements of the AP and also the previous measurements of its highly correlated neighbours to predict  the future value of this specific metric. Otherwise, the proposed methodology makes a temporal based prediction using the 𝐿 previous measurements of this AP
* Data prediction:
  * With the data, an offline training is done in order to obtain a function that will be used in the prediction step
  * For the AP that has highly correlated neighbors, the training is done by using the previous measurements of the corresponding AP and also its corresponding neighbors. 
  * For the AP with no highly correlated neighbors, the training is done only by using the previous measurements of the corresponding AP.
* Prediction techniques:
  * Since, the number of highly correlated neighbors may be different for each AP and time series techniques typically require fixed-size input data, the author utilize padding/truncation method to ensure a consistent input size
  * The author determine maximum value for neighbors for each AP. If the actual number of neighbor of the AP is higher, the algorithm selects the neighbor APs with the highest correlation and discards the rest
  * Otherwise, if the actual number of neighbour APs is less than the maximum value of neighbors, the algorithm pads the input data with zeros for missing features corresponding to non-existent neighbours
  * Both traditional, e.g. Autoregressive Integrated Moving Average (ARIMA) and modern methods, e.g. Long Short Term Memory (LSTM) are used for training time series.
* Algorithms used:
  * ARIMA Algorithm: AutoRegressive Integrated Moving Average (ARIMA) algorithm is a popular time series prediction method. In this paper, the author apply ARIMA to measurements of the target AP using a two-step process. First, the appropriate model order is determined using the auto-arima function. Once the optimal order is identified, ARIMA is used with that specific order along with the ‘‘Recursive Sampling’’ technique to improve prediction performance. This method is utilized only for temporal prediction.
  * RNN Algorithms: Recurrent Neural Networks (RNN) are a class of models effective for time-series prediction due to their ability to recurrently utilize previously processed data, improving prediction accuracy. The RNN techniques thas are used are SimpleRNN (SRNN), Long Short-Term Memory (LSTM) and Gated Recurrent Unit (GRU). SRNN ability to retain long-term information are limited, while LSTM has better control over data flow and memory retention. However, LSTM requires more computational resources and time due to its complexity. Gated Recurrent Unit (GRU), a variant of LSTM, reduces computational complexity but may sacrifice some long-term memory capacity. A comparison of the RNNalgorithms is performed for both temporal and spatio-temporal prediction
  * CNN Algorithm:  A possible way to adapt the input data for Convolutional Neural Network (CNN) algorithm is to divide the sequence into multiple input/output patterns, where a certain number of time steps are used as input and a time step is used as output to predict the next step. CNN is used for both temporal and spatio-temporal prediction.
  * CNN-RNN hybrid algorithm: This architecture, only used for spatio-temporal prediction, combines CNN and RNN to leverage CNN’s spatial feature learning and RNN’s temporal dependency capture. Figure below illustrates the proposed architecture that combines CNN and RNN. From the figure, it can be seen that the CNN architecture integrates the temporal measurements of the 𝑖th AP and its 𝑀 highly correlated APs to analyse spatial dependencies. TheCNN output serves as input for the subsequent RNN phase to predict the metric’s value in the subsequent time period.
    ![alt text](assets/images/spatio-temporal%20prediction/CNN-RNN.png)
  * Transformer algorithm: This model is utilized for both temporal and spatio-temporal prediction. The architecture of the model consists of an encoder and a decoder stack. The available data is used as input to the encoder while the decoder operates on the sequence input to produce the decoder output.

### Experiments
For the evaluationy, real measurements were collected from a total of 100 APs deployed in a University Campus of Universitat Politécnica de Catalunya, located in Barcelona during three months. The collection and management of the measurements is done by means of the Cisco Prime Infrastructure [43]. This tool periodically collects a large amount of AP measurements to capture the network status and centralizes all this information for building statistics useful for prediction purposes, etc. 

The prediction methodology is used here for the prediction of future AP traffic values and transmission failures. The data is preprocessed in a form of time series data for each AP, separately. The prediction methodology makes use of the measurements collected during the weekdays between September 9th, 2019 and December 22th, 2019 from 5:30 to 22:00 for every day with a periodicity 𝑇 = 30 min. This corresponds to 34 time periods per day, resulting in a total of D = 75 days and N = 2550 measurements for each metric.

After pre-processing, the measurements of traffic load and transmission failures for each single AP are obtained. The normalized traffic load is calculated as the number of transmitted packets in each time period (𝑇𝑥𝐶) normalized by the maximum observed value in the measurements data (𝑀𝑎𝑥𝑉). On the other hand, the traffic transmission failures are calculated as the ratio between 𝐹𝑇𝑥 and 𝑆𝑇𝑥 times 𝑆𝑇𝑥𝑅 , 𝐹𝑇𝑥, 𝑆𝑇𝑥 and 𝑆𝑇𝑥𝑅 represent the number of failed transmitted packets, the number of successfully transmitted packets and the number of successfully transmitted packets after retransmissions, respectively..

The features that are used for training:
* Time: this corresponds to the timestamp when the measurements have been taken (date/time).
* AP_name: this feature is related to the name of AP (string).
* Radio_type: it indicates the radio interface where the measurements are taken (string).
* Number of transmitted packets (TxC): this metric is a counter that is increased every time a MSDU (MAC Service Data Unit) is transmitted (integer).
* Number of successfully transmitted packets (STx): this metric is a counter that is increased every time a MSDU is transmitted successfully without the need of retransmission (integer).
* Number of successfully transmitted packets after retransmissions (STxR): this is a counter that is increased every time a MSDU is successfully transmitted after one or more retries (integer).
* Number of failed transmitted packets (FTx): this metric is a counter that is increased every time a MSDU frame is not transmitted successfully after a maximum number of retransmission attempts (integer).

The features will be preprocessed and normalized as explained before,  the author selected M = 5 as the maximum number of neighbours because considering the five most correlated neighbour APs captures sufficient spatial dependencies for accurate predictions without overwhelming the model with excessive information. Following the dataset preprocessing for each RNN, CNN, and Hybrid model implementation, a validation method called walkforward validation is used. It is suitable for time series data with a 0.3 percentage split. The model is trained by using past data and is validated on the next data point. This process is repeated by updating the training set each time with the most recent data. This helps the model adapt to changes in the time series pattern. The hyperparameters that yield the optimal average result across all validation windows are then selected for the ML prediction models.

The result of the training will be compared. The comparison primarily focuses on evaluating prediction accuracy of the different algorithms. The prediction accuracy is assessed using various metrics, including the R2 Score, Mean Square Error (MSE), Root Mean Square Error (RMSE) and Mean Absolute Error (MAE). The Computational Time (CT), which is the training (TCT) per second, is also compared. 

Hyperparameter tuning is also a crucial step in optimizing the prediction accuracy of DL algorithms. In this paper, the author focused on tuning the hyperparameters that have the most significant impact on prediction accuracy.
* For CNN,a configuration with 16 kernels and 2 layers exhibited the highest accuracy across the experiments. 
* For RNN, a configuration with 50 cells in each of the 2 layers demonstrated superior performance and was chosen as the optimal configuration. 
* For CNN-RNN, a configuration with a batch size of 16 and 100 epochs achieved the highest performance comprised 

### Result
These are the results of prediction of each model:
* Temporal Prediction
  
![alt text](assets/images/spatio-temporal%20prediction/Temporal%20traffic.png)
![alt text](assets/images/spatio-temporal%20prediction/Temporal%20failure.png)

As shown in the tables, all the methods yield highly accurate predictions. LSTM stands out slightly with better performance compared to other algorithms. LSTM provides the best prediction accuracy since it has an intrinsic ability to retain memory and capture sequential dependencies that allows it to model these complex relationships effectively.CNN has the worse prediction accuracy because CNN is more adequate for space-based predictions and it is not so suitable for temporal-based prediction.

*  Spatio-temporal prediction

![alt text](image.png)
![alt text](image-1.png)

As shown in the Tables, the results obtained by the spatio-temporal LSTM, CNN and GRU methodologies provide higher prediction accuracy. the hybrid CNN-LSTM model achieves the highest prediction accuracy for both traffic usage and failures of a target AP. Note also that CNN-SRNN provides a relatively high prediction accuracy with a considerably lower TCT than CNN-LSTM. The PCT for both single and hybrid NN models exhibits minimal difference or is closely matched.

After we get the best model, we can use it for future prediction, either traffic or failure. By accurately forecasting the network metrics such as traffic load and transmission failures, this methodology aims to optimize resource allocation, proactively address maintenance issues, and plan for future capacity needs. This proactive approach not only enhances network reliability and performance but also improves the overall user experience by minimizing downtime and congestion. 

Implementing this methodology in a real network involves defining and addressing Key Performance Indicators (KPIs) that are relevant to the specific network environment and operational requirements. KPIs such as TCT, PCT, prediction accuracy are essential metrics to consider when evaluating the performance of prediction methods in a real network setting. The TCT for training the models was relatively low across all methods, facilitating fast offline training and retraining processes. This ensures that models can be updated frequently. The PCT for both temporal and spatio-temporal prediction was found to be minimal, allowing for almost real-time predictions.

For the scalability involving a greater number of APs (i.e. addition of new APs), it is necessary to collect data for each new AP and its neighbours, pre-process (fill missing data, etc.), calculate correlations and execute trained model. Furthermore, in this scenario, adapting to new circumstances may entail either fine-tuning the model’s trainable parameters or completely retraining it. 


### Conclusion:
Prediction of future values of network metrics (such as future traffic values at the APs, future obtained performance metrics, etc.) can be useful to make proactive decisions over the network by means of e.g. load balancing, proactive resource allocation, congestion control, etc., that can improve the network performance. This paper has proposed a new methodology for the prediction of future values of some specific parameters according to historical measurements and by leveraging space correlations among neighbouring APs. 

The proposed prediction methodology relies on Neural Networks and operates in two steps. First, the collected historical data is used to train the model in an offline process. Then, newly collected data is input into the trained model during the prediction step. Different DL methods have been analysed, including SimpleRNN, CNN, GRU, LSTM and Transformer for both temporal and spatiotemporal prediction tasks. Moreover, hybrid DL algorithms have been proposed, consisting of an initial CNN process to extract spatial correlations and a subsequent RNN step to exploit temporal correlations. 

The proposed methodology has been tested using real data obtained from a Wi-Fi network deployed on a University Campus to predict future AP traffic and transmission failures. The proposed methodology with the hybrid DL methods obtains high prediction accuracy (i.e. average R2 score up to 93.7% and 92.4% for traffic load and failures, respectively) with a relatively small TCT (i.e. in the order of hundreds of seconds) and a reduced PCT (lower than 2 s). In particular, exploiting the spatial correlation among neighbouring APs results in higher prediction accuracy for spatio-temporal predictions. The PCT values for both the temporal and spatio-temporal prediction NN models remain very similar, it means that it can provide real time prediction.


## Virtual reality traffic prioritization for Wi-Fi quality of service improvement using machine learning classification techniques

Shaabanzadeh, Seyedeh Soheila, et al. "Virtual reality traffic prioritization for Wi-Fi quality of service improvement using machine learning classification techniques." Journal of Network and Computer Applications 230 (2024): 103939.

### Background:
Latency is a significant issue in Virtual Reality (VR), both in wired and wireless systems. In VR services, a too high latency may cause that the gap between the VR video game and what the user sees becomes excessively large. This gap can lead to motion sickness and degrade the perceived user quality of experience.  Wi-Fi QoS management can significantly enhance user experiences by reducing latency and jitter in real-time applications like gaming, preventing disruptions in immersive experiences, and minimizing lag during access to cloud and edge services

The increasing demand for high data transmission has led to extensive research in creating new mechanisms to identify and classify network traffic. In essence, a precise traffic identification procedure allows the efficient management of existing network resources, thereby permitting more accurate and robust resource allocation schemes.


### Proposed Solution: 
This paper proposes an interactive VR ML traffic classification model in the edge streaming VR scenario. The proposed model evaluates the use of some common classifiers, fed with the features previously extracted, such as flow duration, packet length variance, maximum and minimum segment sizes, window size, round trip time, and packet inter-arrival time. The model is evaluated by using VR traffic traces coming from a multi-user VR scenario, and using single-user traces from a VR framework not included in the training traces. Finally, a Wi-Fi network environment is simulated in order to illustrate how the model can be used to detect VR traffic, and give it higher priority to improve its QoS. In particular, the key contributions of this study are as follows:


### Methodology:
This section describe about the process for the generation of the datasets, selection of the features used for classification, the design of the proposed classifiers, and the aspects related to the tuning the hyperparameters of the
considered classifiers.

1. Dataset creation
  
  The dataset that is used in this paper consists on two different traffic
datasets, one for VR traffic and one for Non-VR traffic. The
first VR traffic dataset is related to a range of VR application in various different configurations. The second dataset representing Non-VR traffic focuses on commonly used application types such as non-game videos , and online meetings. 
   * Network Setup: The network setup consists of a Desktop computer connected to the Access Point (AP) that supports Wi-Fi 6 with an ethernet cable and the clients are connected to the AP via Wi-Fi access point (AP).For VR, The desktop will act as VR server which send downlink data, and the Head Mounted Devices (HMD) will act as VR client which send uplink data to the server. 
   
      For Non-VR, the laptop connected to the AP linked to the internet will stream multimedia services. The streaming operation involves sending requests for video and audio content as UL data and in response, downloading video content from multimedia servers as DL data.  Figure below is the network setup
  ![alt text](assets/images/VR%20classification/setup.png)
    * Data Collection: VR and Non-VR traffic data are collected respectively in Desktop and laptop. Wireshark is utilized to gather raw traffic data and to save as .pcap files.  During the data collection process, other applications are shutted down to minimize interference. 
    * Feature Engineering: For feature extraction, first, the author define some short periods of time. Each set of packets within a period is called a ‘sample’. For each sample, the DL and UL data are separated, and then Number of Packets, Total Bytes and statistics such as Minimum, Maximum, Mean, and Standard Deviation for Packet Size and Packet Interarrival Time, are computed for both DL and UL, separately. Besides, of that, the author also added 3 features, which are Ratio of Number of Packets, e Ratio of Total Bytes, and cross correlation, which is calculated from pearson corelation. In addition to extracted features, a binary label is also included in the dataset to identify VR from Non-VR


      For feature selection, the author use filter selection using a feature importance method, called permutation importance that is both model-agnostic and easily comprehensible. Based on permutation importance feature selection technique, the importance of each feature has been obtained in each specific dataset with a single sample duration, specific correlation subsample and for each ML classification algorithm.

 
2. Traffic classification methods

Traffic classification methods are essential for managing and optimizing network performance by identifying the types of traffic flowing through the network. Below are the classification methods that are used:

* LR: a linear classification algorithm used for binary or multi-class classification that models the probability of an instance belonging to a particular class using a logistic function
* SVM: a versatile algorithm for classification that finds a hyperplane for best separating data points of different classes in classification 
* kNN: a simple instance-based learning algorithm that classifies data points based on the majority class among their k nearest neighbors.
* DT: a tree-like structure where each node represents a decision based on a feature.
* RF: an ensemble method that consists of multiple decision trees that improves upon the weaknesses of individual decision trees by aggregating their predictions. 
* NB: a probabilistic classification algorithm based on Bayes’ theorem that assumes independence between features (a ‘‘naïve’’ assumption) and calculates the probability of an instance belonging to a class. NB is simple and efficient


### Experiments
1. Hyperparameter Tuning

    The considered hyperparameters by using GridSearchCV framework, which   incorporates a robust cross-validation approach with a fixed count of three, are listed as below:
   * ‘‘LR_parameters’’: [‘‘solver’’: [‘liblinear’, ‘saga’], ‘C’: [0.1,1]]
   * ‘‘SVM_parameters’’: [‘kernel’: [‘rbf’,‘sigmoid’], ‘C’: [0.1, 1]]
   * ‘‘kNN_parameters’’: [‘n_neighbors’: [5,10], ‘weights’: [‘uniform’, ‘distance’]]
   * ‘‘DT_parameters’’: [‘min_samples_split’: [5,8], ‘max_depth’: [5,10]]
   * ‘‘RF_parameters’’: [‘n_estimators’: [5,20,50], ‘min_samples_split’: [5,8], ‘max_depth’: [5,10]]
   * ‘‘NB_parameters’’: [‘var_smoothing’: np.logspace(0,-9, num = 100)]

2. Classification Result

    After doing hyperparameter tuning for each of the method, the data are then classified. Table below is the result of the classification:

    ![alt text](assets/images/VR%20classification/result.png)
    
    From the result, it can be seen that RF classifier has the most accurate prediction followed by DT. These two models will be used for classifying the traffic to prioritize for VR traffic

3.  Testing the model
      
      The classification model is tested using packet traces of three users playing VR games in a multi-user experimental setup like shown in figure below.
      
      ![alt text](assets/images/VR%20classification/testing%20the%20model.png) 
      
      For each user, in label prediction, first the feature extraction model is applied on packet arrivals to obtain samples in which the features are computed and then, the classification model to obtain whether the model can correctly predict its type or not. From 128 samples of the first user  that was playing a VR game, 127 samples are correctly classified and only one is misclassified when applying the RF classifier, while with DT, 126 samples are predicted in a correct class and 2 misclassified. For computational time, it takes approximately 0.7670 s for feature extraction and 0.0131 s for classification using a DT classifier. The computational time increases slightly to 0.0240 s when using a RF classifier. Thus, the total computational time remains below 1 s for each sample.

4. Wi-Fi QoS enhancement through the prioritization of VR traffic

      In this section, network simulator will be used to analyze the impact that VR traffic identification can have in current Wi-Fi networks. We employ an extended version of the C++ simulator, which allows to simulate Wi-Fi 6 networks. The scenario consists of an Access Point (AP) and two Stations (STAs). The following MCS are used: 1024-QAM 5/6 for the first STA, and 256-QAM 5/6 for the second one, both use 80 MHz channels on the 5 GHz band. The first STA is using VR and the  second STA is receiving non-VR background traffic. 
      
      To showcase the impact that traffic identification can have in Wi-Fi QoS, the AP will detect whether the traffic is VR or BG, and prioritize the first one accordingly, ignoring all BG packets until all VR packets are transmitted. After applying the classification model and determining the sample is VR, all arriving packets with the same source and destination IP will receive high priority from the AP and will be transmitted

      ![alt text](assets/images/VR%20classification/system%20operation.png)

      Figure below shows the median and worst-case packet delay (99th percentile) for both VR traffic and BG traffic with and without VR prioritization active in the DL. Once VR prioritization is active, VR delay decreases in all cases, and for 400 Mbps we can observe a 76.27% decrease, leading to a delay of less than 10 ms, and a smoother experience for the player. For BG traffic on the other hand, prioritization leads to an increase in the delay. Prioritizing one type of traffic will lead to worse delays for other traffic types. However, BG traffic could be a file download or video streaming through Youtube, which either do not have strict latency requirements (former) or can compensate through the use of buffering (latter), which VR traffic cannot use. With this approach, VR traffic delays is 4.2x lower than without prioritization, with only a 2.3x higher delay in the BG traffic
      ![alt text](assets/images/VR%20classification/comparison.png)

### Conclusion:
Interactive XR/VR traffic identification over Wi-Fi can be helpful to decrease latency for XR users, improving network QoS and user experience. In general, this paper demonstrates that the ML-based traffic classification method offers a compelling balance between accuracy and computational efficiency. In our testing phase using the DT or RF classifier, we achieved an accuracy higher than 0.984 with a computational time under 1 s per sample. This indicates that the computational time is moderate, making it suitable for long-lasting real-time applications. Secondly, a network simulator is utilized to investigate the potential impact of VR traffic identification in existing Wi-Fi networks. In a scenario involving an AP and two Stations (STAs), the first STA engaged in playing a VR game using ALVR, while the second STA received non-VR background traffic. The AP was configured to detect whether the traffic is VR or BG, and prioritize VR traffic, disregarding BG packets until all VR packets were transmitted. With this prioritization approach, we achieved VR traffic delays 4.2 times lower than without prioritization, accompanied by only a 2.3 times higher delay in the BG traffic.


## Title


### Background:


### Proposed Solution: 

### Methodology:

### Experiments

### Conclusion: