# Power Side-Channel Malware Detection Dataset
This README describes the contents and utilization of the Power Side-Channel Malware Detection dataset.


Power traces were collected from a Portwell PCOM-C700 Type VII carrier board with a Portwell PCOM-B700G processor module.
This module features an 8-core Intel Xeon D-1539 embedded-class processor.
Sampling was performed using a YHDC HSTS016L Hall-effect split core current Hall-effect current sensor clamped around the 12V CPU power cable.
Current sensor readings were recorded using a PicoScope 2408B oscilloscope at a sampling rate of 2 KHz.  


Each trace samples one operating state; a permutation of executing applications.
Traces feature both uninfected and infected counterparts of each state.


## Paper
More technical details are available in our paper published in HASP 2024.(SoK Paper: Power Side-Channel Malware Detection);


## Instructions
All traces are provided as a timeseries csv in a flat directory.
Users are responsible for preprocessing and train-test splits.


### Format
Traces are provided in csv format and labelled {state}\_{attack}\_2024\_{index}.csv
State refers to the unique combination of executing benign applications.
Attack specifies which attack (malware) is executing in parallel with the state.
Index is used to order traces of the same state and attack. 


### Applications and Malware
#### Benign Applications
**hash**
SHA-3 implementation from the Extended Keccak Code Package [link](https://github.com/XKCP/XKCP).

**facedetect**
A face detection application using the [OpenCV](https://docs.opencv.org/4.x/index.html) library running a [video benchmark](https://arma.sourceforge.net/chokepoint/). 

**package-delivery**
Autonomous drone package delivery benchmark from [MAVBench](https://github.com/harvard-edge/MAVBench).


#### Malware
[Meltdown](https://meltdownattack.com/) [Proof of concept](https://github.com/IAIK/meltdown) 
Specified in trace naming as: \_m\_


[Spectre](https://meltdownattack.com/) [Proof of concept](https://github.com/crozone/SpectrePoC)
Specified in trace naming as: \_s\_

L1-Cache Covert-Channel [link](https://github.com/casenh/covert-channels)
Specified in trace naming as: \_cc\_

When no malware is executing, a state is considered benign and specified in trace naming as \_b\_.


### States
s0: ----------------, ----------, ----  (idle)

s1: ----------------, ----------, hash 

s2: ----------------, facedetect, ---- 

s3: ----------------, facedetect, hash 

s4: package-delivery, ----------, ---- 

s5: package-delivery, ----------, hash 

s6: package-delivery, facedetect, ---- 

s7: package-delivery, facedetect, hash 

### Legend
Traces are provided in csv format and labelled {state}\_{attack}\_2024\_{index}.csv

s0\_b\_2024\_00.csv refers to the first trace collected from benign state 0.

s0\_b\_2024\_01.csv refers to the second trace collected from benign state 0.

s1\_b\_2024\_00.csv refers to the first trace collected from benign state 1.

s1\_m\_2024\_00.csv refers to the first trace collected from state 1 when infected by Meltdown.

s1\_cc\_2024\_00.csv refers to the first trace collected from state 1 when infected by L1-Cache Covert-Channel.






