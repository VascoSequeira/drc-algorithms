# Data Rate Change Algorithms for Efficient HF Communications
This is the location of the Data Rate Change (DRC) algorithms simulation environment.The main purpose of a DRC algorithm is to select the highest possible data rate, based on the channel conditions (e.g., measured BER and/or SNR at the receiving side), and to change that data rate based upon changing channel conditions. The DRC algorithms were used in a HF data transmission between two stations located in Lisbon and Oporto, using the RF-1936P dipole antenna and the military radio E/R GRC-525. In recent years, some DRC algorithms were implemented, but this technology was poorly developed with only two structured algorithms: Trinder [1] and RapidM DRC algorithm 1 [2]. Based on the assessment results, several improvements on those algorithms are then proposed and evaluated by implementing the Avoiding Cut-Off State (ACOS) and Bit Error Optimization (BEO) algorithms.

In order to assess the performance of the existing DRC algorithms, a simulation environment was created in Matlab code, whose flowchart is presented in the Dissertation pdf file. The simulation system starts with an initialization process that loads the SNR channel requirements for a BER of 10−5 and for the considered channel type, which can be AWGN, ITU Good or ITU Poor. These SNR requirements are defined according with the NATO standards – STANAG 4539 [3] and STANAG 4285 [4], and MIL-STD 118-110B [5].  This process continues with the reading of the current channel SNR, which leads to the computation of the initial data rate by comparing the current SNR with the SNR channel requirements.

After the initialization process, the data transmission between stations starts. Periodically, the system reads the current channel SNR and computes the corresponding channel BER and FER; based on these values and on the current data rate, a new data rate value is computed by the DRC algorithm that will be applied to the following transmission interval. After the BER and FER computation, the selected DRC algorithm will be applied whenever there is still data to be transmitted; the current data rate will then be updated for the following data transmission interval.The equations to compute these values can be consulted in the Chapter 5 of the Dissertation pdf file. 

Based on detected vulnerabilities of the Trinder and RapidM algorithms, two new versions of each algorithm were developed and tested in the Matlab simulation environment; the first improved version performs a BER prediction to avoid the cut-off link, and was named Avoiding Cut-Off State (ACOS); the second improved version performs an average BER optimization, and was named Bit Error Optimization (BEO). 

The ACOS algorithm is implemented before the Trinder or RapidM, and it starts with the new BER computation based on the new data rate selected by the DRC algorithm. After performing the BER prediction, the algorithm verifies if the resulting BER value is greater than 10−3; if it is false, the data rate is updated to the new value; if this condition is true, a new verification is performed. The algorithm checks if the new data rate is lower than previous one; if it is false, the previous data rate is maintained; if it is true, the new data rate is decreased. 

The main difference between ACOS and BEO algorithms is the condition block. In the ACOS algorithm, the condition avoids the link cut-off. In the BEO algorithm, if the predicted BER value is lower (or equal) than the BER threshold, defined in the original algorithms, the data rate is updated, otherwise a new condition is verified. This new condition checks if the new data rate is lower than the previous data rate. If this is true, the data rate should decrease, otherwise the previous data rate is kept

To assess the algorithms, four types of channel SNR variations have been considered: downward sinusoidal, upward sinusoidal, sinusoidal and step-wise. All these variations were tested with the three types of channel classification: AWGN, ITU Good and ITU Poor. Seventy two different cases were assessed, whose results can be consulted in the Dissertation pdf file, and the respective code in the Matlab file.

# Source Publication
Please cite the following paper in your publications, if you have used any content of this site, in your work:

Vasco Sequeira, Maria Paula Queluz, António Rodrigues, José Sanguino, Pedro Grifo, "Data Rate Change Algorithms  for Efficient HF Communications",  Int. Conf. on Military Communications and Information Systems,  ICMCIS 2018, Warsaw, Poland, 22-23 May 2018

# References
[1] S. Trinder and A. Gillespie, “Optimisation of the STANAG 5066 ARQ Protocol to Support High Data Rate HF Communication,” in Proceedings of IEEE Military Communications Conference (MILCOM) 2001, Washington, DC, October 2001.

[2] S. Schulze and G. P. Hancke, Design and Implementation of a STANAG 5066 Data Rate Change Algorithm for High Data Rate Autobaud Waveforms,  Pretoria, South Africa: Department of Electrical, Electronic and Computer Engineering, University of Pretoria, 2005.

[3] STANAG 4539, Technical Standards for Non-Hopping HF Communications Waveforms, NATO, 2000.

[4] STANAG 4285, Characteristics of 1200 / 2400 / 3600 bits/s Single Tone Modulators / Demodulators for HF Radio Links, NATO, 1989.

[5] MIL-STD-188-110B, Interoperability and Performance Standards for Data Modems, Department of Defense United States of America, 2000.
