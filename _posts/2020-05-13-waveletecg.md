---
title: 'Real Time Wavelet Filtering for ECG Baseline Wander Removal'
date: 2020-05-13
permalink: /posts/2020/05/waveletecg/
tags:
  - research
  - signal processing
  - wavelet
---

I worked on this project during the second semester of my junior year under the supervision of <a href="https://scholar.google.co.in/citations?hl=en&user=TrujKPcAAAAJ&view_op=list_works">Dr. Ananthakrishna Chintanpalli</a>.</p> 

**Briefly explain the problem you worked on.**
<p style='text-align: justify;'>
The problem I worked on is the removal of the baseline wander from electrocardiogram (ECG) signals using wavelet-based filtering in real time. </p>

<p align="center">
  <img src="https://akulmalhotra.github.io/files/waveletecg/ecg.jpg?raw=true" alt="Photo" style="width: 450px;"/> 
</p>

<p style='text-align: center;'>
Figure 1: The P/Q/R/S/T components of an ECG signal </p>

<p style='text-align: justify;'>
An ECG signal measures the activity of the heart over a period of time. It provides information about the person’s heart rate and rhythm, and is used to detect various heart disorders such as hypertension (high blood pressure) and irregular heart rhythm (arrhythmias). Figure 1 <a href="https://en.wikipedia.org/wiki/Electrocardiography">[1]</a> shows the various segments of the ECG signal for 1 cardiac cycle. To record a person’s ECG,  sensors are attached to the person’s chest and limbs, which transmit the recorded signals onto a computer, where further processing can be done.  ECG signals are often contaminated with various kinds of noise during the data acquisition process. Baseline wander is a low frequency (0-0.5Hz) noise that is caused due to body movement and respiration during data collection. </p>

<p style='text-align: justify;'>
Since ECG signals are used for medical diagnosis, and incorrect diagnosis due to noise in the signal is simply unacceptable. Therefore, various signal processing techniques are applied to the recorded ECG signal to remove the noise from it. Wavelet-based filters are a popular technique to eliminate the baseline wander from ECG signals. I’ll talk more about these filters later. </p>

<p style='text-align: justify;'>
Signal processing techniques like wavelet-based filters are generally computationally expensive algorithms that take a lot of time to run on general-purpose computers. This problem is further worsened when the collected data is of large size, which is normally true for biomedical signals like the ECG signal. </p>

<p style='text-align: justify;'>
The problem I was trying to solve was to reduce the time taken for the baseline wander removal, by using special-purpose hardware (DSP kit). </p>

**Why is solving this problem important/ How is solving this problem beneficial?**

<p style='text-align: justify;'>
Faster processing of the collected data would lead to faster diagnosis, which can be beneficial in multiple ways. A reduction of diagnosis time would enable doctors to make decisions faster, which can be crucial in emergency situations. Also, faster processing means fewer ECG kits would be required to conduct the same number of tests as before, leading to a reduction in costs for the medical facility. </p>

**Please describe your results.**

<p style='text-align: justify;'>
Figure 4 shows the raw input signal with baseline wander, taken from the MIT-BIH Normal Sinus Rhythm Database <a href="https://www.physionet.org/content/nsrdb/1.0.0/">[2]</a>. The signal was passed through the wavelet-based filter as well as the traditional filters. Filtering was done both on the DSP kit and MATLAB for comparison and validation of the results. Figure 5 shows the output of the wavelet-based filter using the DSP kit. It can be seen that the baseline wander has been removed without impacting the desired components of the signal. The results of filtering with the traditional filters can be found in the paper. </p>

<p align="center">
  <img src="https://akulmalhotra.github.io/files/waveletecg/raw.jpg?raw=true" alt="Photo" style="width: 450px;"/> 
</p>

<p style='text-align: center;'>
Figure 4: Raw ECG signal </p>

<p align="center">
  <img src="https://akulmalhotra.github.io/files/waveletecg/filtered2.jpg?raw=true" alt="Photo" style="width: 450px;"/> 
</p>

<p style='text-align: center;'>
Figure 5: Filtered ECG signal using the wavelet-based filter </p>

<p style='text-align: justify;'>
<b>What are some papers/resources that you would recommend others to read so that they can get to know more about this field? </b></p>
