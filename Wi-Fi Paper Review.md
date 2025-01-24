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




## Title

### Background:


### Proposed Solution: 

### Methodology:

### Experiments

### Conclusion: