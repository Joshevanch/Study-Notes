# Nvidia Sionna (v0.8.0)

## Background

Some of the most prominent 6G research topics are communication in the Terahertz band, cell-free, holographic, and very large aperture multiple-input multiple-output (MIMO), unmanned aerial vehicle (UAV) and satellite communication, machine learning (ML)-based air interface design, semantic communication, reconfigurable intelligent surfaces (RIS), sensing and localization, digital twins, computer vision for wireless, as well as federated learning over wireless. Research on most of the above topics requires one or more of the following:
* **Data from specific radio environments**: Radar-based sensing and localization as well as computer vision-aided applications only work if there is a spatially consistent correspondence between physical location and channel impulse response (or visual input). This can only be achieved through either ray tracing or extensive measurement campaigns
* **Native integration of ML**: ML and, particularly, neural networks (NNs) are expected to play an increasingly important role for the implementation of transceiver algorithms and maybe even the 6G air interface design. Research on such topics benefit tremendously from a tight integration of ML, link-level simulation tools, and also fromautomatic gradient computation through the entire systemwhich allows for seamless integration of NNs.
* **Very high detail or scale**: Link-level simulations of 6G systems require unprecedented modeling accuracy and scale. While cell-free or very large aperture MIMO systems need the computation of a very large number of signal propagation paths, Terahertz communication systems have complex channel models accounting for nonlinear hardware impairments.

Due to the reasons above, that the breakthroughs required for 6G can  be achieved if the community has access to new tools for physical layer research. That is the authors have started to develop a new and open-source link-level simulator called Sionna.

## Objective
Sionna is written by researchers for researchers in communications and aims at making our work more efficient:
* Rapid prototyping: Sionna provides a high-level Python API to rapidly model complex communication systems from end-to-end while allowing one to easily adapt the parts a new research idea is about.
* Benchmarking against the state of the art: Sionna provides many carefully tested standard processing blocks and state-of-the-art algorithms that can be used for performance benchmarking. This reduces the time spent implementing auxiliary components that one’s research is not about.
* Realistic industry-grade evaluations: one can make evaluation of algorithms for end-to-end performance with a few additional lines of code. If needed, simulations can be scaled across large multi-GPU setups.
* Native support of NNs: Sionna enables seamless integration of NNs in the physical layer signal processing chain. As most building blocks are differentiable, gradients can be backpropagated through an entire system, which is the key enabler for end-to-end learning AI-defined air interfaces. Sionna also eliminates the need for different tools for data generation, training, and evaluation.
* Addressing 6G research needs: Sionna will allow for the use of ray tracing, datasets, and generative models instead of stochastic channel models to enable research on many novel topics, such as joint communication and sensing, vision-aided wireless communications, intelligent reflecting surfaces, semantic communications, and digital twins.
* Reproducibility: With Sionna, it is straight-forward to make research reproducible by others. We encourage all users to publish their Sionna-based code along with their research papers and contribute novel components so that they can be reused by others. This will also make it easier to compare algorithms under the same conditions.

### Sionna Primer
Sionna is written in Python using TensorFlow and the Keras API. All Sionna algorithms are implemented using high-dimensional Tensors where the first dimension is the batch size, representing different independent Monte Carlo trials that are executed in parallel. 

Another design principle of Sionna is that all components are implemented as independent Keras layers. This has the
advantages that 
* complex system models can be constructed by simply connecting the desired layers
* components can be easily replaced by NNs
* gradients are automatically computed by TensorFlow which is a key enabler for end-to-end learning of communication systems. Both Keras’ sequential and functional APIs can be used.

### Features
The first public release of Sionna (v0.8.0) implements the
following list of features:
* **Forward error correction (FEC)**:
    * 5G LDPC codes including rate matching
    * 5G Polar codes including rate matching
    *  Cyclic redundancy check (CRC) 
    *  Reed-Muller & Convolutional codes
    *  Interleaving & Scrambling
    *  Belief propagation (BP) decoder and variants
    *  SC, SCL, and SCL-CRC Polar decoders
    *  Viterbi decoder
    *  Demapper with prior
    *  EXIT chart simulations
    *  Import of partity-check matrices in alist format
* **Channel models**:
    * Additive white Gaussian noise (AWGN) channel
    * Flat-fading channel models with antenna correlation
    * 3GPP 38.901 TDL, CDL, UMa, UMi, RMa models
    * Import of channel impulse response from datasets
    * Channel output computed in time or frequency domain
* MIMO processing:
    * Multiuser & multicell MIMO support
    * 3GPP 38.901 & custom antenna arrays/patterns
    * Zero forcing (ZF) precoding
    * Minimum mean squared error (MMSE) equalization
* Orthogonal frequency-division multiplexing (OFDM):
    * OFDM modulation & demodulation
    * Cyclic prefix insertion & removal
    * Flexible 5G slot-like frame structure
    * Arbitrary pilot patterns
    * LS channel estimation & Nearest neighbor interpolation


