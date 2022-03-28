# Accurate 3D Localization for MAV Swarms by UWB and IMU Fusion

## Abstract

UWB, impressive performance in both indoor, but high latency and low bandwidth.

Extended Kalman Filter (EKF) based algorithm is proposed to fuse the Inertial Measurement Unit (IMU) and UWB, which achieved 80Hz 3D localization with significantly improved accuracy and almost no delay. 

6 MAVs is set up to perform a light show in an indoor exhibition hall, to verify the effectiveness and reliability of the proposed approach.

Video and source codes are available at [https://github.com/lijx10/uwb-localization*]





## I. Instruction

Micro Aerial Vehicle (MAV)  微型飞行器

Micro Aerial Vehicle (MAV) swarm 微型飞行器群



1. The accuracy of standard **GPS** is meter-level and it can be boosted to centimeter-level, when running as Real Time Kinetic (RTK) mode with an additional fixed base station.

2. **VICON** system provides centimeter-level accuracy in indoor environment but it requires an expensive and complex setup with multiple cameras.

3. Vision based solution is of particular interest because it is low-cost, light-weight and flexible. **IMU** is used to improve system robustness in the case of marker detection lost in a short period. heavy computational power and proper lighting condition are necessary, which limits its applications.

4. **Radio based localization systems**. **RFID**(Radio Fre- quency Identification) is widely used in ... However, RFID can only work with a small proximity range and ranging with RSS is only a rough estimate.

   Zigbee... WiFi...



**UWB** is one of the most promising solutions in terms of **accuracy**, **coverage range**(全覆盖范围) and **deployment cost**. 

The range between two UWB nodes can be determined by the **time difference of arrival (TDOA)**[17], [18]. 

At the same time, high capacity data transmission can be implemented with small energy consumption.

Therefore, UWB is an excellent high-accuracy positioning system for MAV swarms in GPS-denied environments.



## II. SENSOR SETUP

UWB sensors manufactured by TimeDomain (shown in Fig. 1) are set up as a **two-way ranging system**. 

**6 UWB sensors** are fixed in the exhibition hall as anchors(宽度).

build a coordinate system of the anchors by precisely measuring the distances and angles between them.



The **two-way ranging system**, which is also called **Time- of-Arrival (TOA)** system, is configured with the techniques of **Time Division Multiple Access (TDMA)** and **Code Di- vision Multiple Access (CDMA)**.



Each **MAV is equipped with an UWB sensor**, denoted as mobile, that works at a unique channel.



i.e. In every 6 time slots, a mobile will **probe all 6 anchors** and get the 

1) respective distance measurements **rk** and the

2)  measurement uncertainty **σrk**

In our setup, **each mobile gets 80 measurements per second**.



## III. VANILLA EKF FOR UWB

Typical TOA based algorithms include multi-dimensional scaling (MDS), weighted least square(加权最小二乘), trilateration(三边测量),these approches requires at least 3 measurements to determine the 3D position, buit in a typical UAB setup, each mobile receives one distance measurement at a time, which means that any three measurements are acquired with different time-stamps. On the other hand, filtering based approaches, such as EKF and particle filter, are able to consume one measurement at a time. Howerver, without other information, they are usally udner some motion assumptions like constant velocity model, which leads to inaccurate or delayed positioning for MAVs.
In a vanilla EKF, the state vector consists of position and velocity defined in (2). Under the constant velocity model, the time update process is defined in (3).

many symbols represents meanings in paper...

severe(严重的) delay can be observed in applications with MAVs, as demonstrated in Section V.


## IV. UWB & IMU FUSION

**To** solve the delay and low bandwidth problem, **fusing** the acceleration information from IMU is an ideal solution.

### *A. Augmented State Vector*

1. an aug- mented state vector x ∈ R9
2. acceleration measurements [ax , ay , az ]T
3. system matrix A
4. input gain Bk−1 and uk−1
5. measurement update Hk

### *B. Implementation Details*

The acceleration from IMU is **fused into** UWB measurements **as the control input**. 

1. the readings from UWB sensors are unstable
2. the IMU readings are quite noisy

=> tend to rely more on UWB readings.

Solution: compute the difference between the predicted distance r ̄k and the actual UWB measurements rk.

dk = |r ̄k − rk|, If dk is over a certain threshold, e.g. 2m, the localization result xk is discarded.

## V. EXPERMENTS

**vanilla KEF** in section 3 and the **fusion EKF** in section 4, are tested in env equipped with VICON system, so ground truth is available and performance of two algorithms can be evaluated. 

Figure 4 and 5 shows, **fusion EKF** singnificantly better *accuracy* and much *lower latency*.

**fusion EKF** deployed on **6 MAVs** that performs a swarming light show at exhibition. 


the UWB sensors are configured to work at two-way ranging mode with TDMA and CDMA. provide distance mesurements between mobiles and anchors at the speed of about 80Hz, and the typical accuracy is 10cm.

The acceleration measurements come from the onboard IMU sensor at the frequency of 50Hz. 

In both test of VICON room and exhibition hall, the 6 MAVs execute a pre-defined path designed by a multi-agent splines based trajectory generation algorithm.

In experiments presented in this paper, only one MAV is used, other 5 MAVs differs only on the path executed. The positioning of MAVs in Section V relies on the fusion EKF algorithm.

### A. VICON Test

UWB anchors(锚) are placed on the ground and the ceiling(天花板). The performance is not ideal but still enough for the MAV to execute a path. vanilla EKF suffers from expetected **overshooting**. 

### B. Performance at Changi Exhibition Centre

the setup with larger space between UWB sensors leads to more stable and accurate estimation. 

difficulties:

1. electromagnetic(电磁) was much more complex with 12 UWB sensors working in full power, as well as thousands of WiFi devices around. 
2. MAVs block the UWB signals of others. Any kind of occlusion(遮挡) may leads to totally incorrect readings.

Both leads to larger ranging error, more frequent measurement jumping. In fusion EKF, apparently incorrect UWB readings are rejected by the innovation thresholding. 

localization accuracy can be evaluated via videos at [https://youtu.be.lid49danIK4]



## VI. CONCLUSION

In this paper, 

1. an **EKF based algorithm** is proposed to **fuse the measurements of UWB sensors and IMU**.

2. **Experiments** with **VICON** system.

3. our approach significantly **outperform vanilla EKF**.
4. the **delay of the localization algorithm** is almost eliminated while vanilla EKF exhibits unacceptable estimation delay
5. multi-MAV light show is performed











## Words

anchor 锚

alleviate 减轻

compensation 补充

miniature 缩略图

picosecond 微微秒

probe 探查

vibration 振动

remedy 救济

augment 增加

swarm 一群

empirically 凭经验

quadrotor 四倍

hover 徘徊

occlusion 遮挡





## 卡尔曼滤波

离散线性卡尔曼滤波，基本卡尔曼滤波算法，适用于解决随机线性离散系统的状态或参数估计问题。

卡尔曼滤波的计算原型：时间更新方程和测量更新方程。











