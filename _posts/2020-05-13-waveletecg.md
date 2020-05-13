---
title: 'Real Time Wavelet Filtering for ECG Baseline Wander Removal'
date: 2020-05-13
permalink: /posts/2020/05/waveletecg/
tags:
  - research
  - signal processing
  - wavelet
---

<p style='text-align: justify;'>
I worked on this project during the second semester of my junior year under the supervision of <a href="https://scholar.google.co.in/citations?hl=en&user=TrujKPcAAAAJ&view_op=list_works">Dr. Ananthakrishna Chintanpalli</a>. </p> 

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

**What are the current state of the art techniques to solve this problem?**

<p style='text-align: justify;'>
Filtering is one of the most used techniques in signal processing. A filter can be described as a device or component which takes a signal as input and removes certain unwanted components from it before outputting it. Since the baseline wander is the unwanted component in the ECG signal, baseline wander removal can be analyzed as a filtering problem. </p>

<p style='text-align: justify;'>
As mentioned earlier, the baseline wander lies between 0-0.5Hz. Therefore, if we remove that particular frequency band, we will get rid of the noise. Another way to interpret that is we let the frequencies in the ECG signal having a value higher than 0.5Hz pass undisturbed while removing the frequency components below it. The filters that perform this operation are called high pass filters. </p>

<p align="center">
  <img src="https://akulmalhotra.github.io/files/waveletecg/idealfilt.jpg?raw=true" alt="Photo" style="width: 450px;"/> 
</p>

<p style='text-align: center;'>
Figure 2: An ideal high pass filter</p>

<p style='text-align: justify;'>
Figure 2 shows an ideal high pass filter, which would zero out all frequency components below x, known as the cutoff frequency. In reality, it is impossible to design ideal filters using traditional filter design techniques. Figure 3 shows 2 real high pass filters designed using the same technique. It can be seen that one filter is more close to the ideal than the other. That is because the order of that filter is higher than that of the other. I won’t go into the mathematical details of the filter order, however, it is essential to know that there is an accuracy-complexity tradeoff associated with it. As we increase the filter order, we get more accurate results but the time it takes to obtain those results increases. Also, designing a filter beyond a certain order sometimes isn’t possible using the conventional design techniques due to the filter becoming unstable. </p>

<p align="center">
  <img src="https://akulmalhotra.github.io/files/waveletecg/realfilt.jpg?raw=true" alt="Photo" style="width: 450px;"/> 
</p>

<p style='text-align: center;'>
Figure 2: Two real high pass filters. The right one has a higher order than the left</p>

<p style='text-align: justify;'>
Generally, traditional filters are sufficient for most real-world filtering applications. This is because a certain margin of error is acceptable in most results. However, in a sensitive industry like healthcare, there is no scope to make incorrect decisions. Therefore, ECG signal processing needs to have near-perfect accuracy. If a traditional filter is used for baseline wander removal, it will need to have a high order to ensure high accuracy, which would dramatically increase the computation time. Therefore, we need to consider other kinds of filters to solve this problem. </p>

<p style='text-align: justify;'>
A wavelet-based filter, inspired by the discrete wavelet transform (DWT), decomposes the original signal into a series of sub-signals. For example, if we have a signal which has a range of frequencies from 0-64Hz, the DWT will decompose the signal into two sub-signals, one with frequencies 0-32Hz, and the other with frequencies 32-64Hz. This process will then be repeated with both the sub-signals. The decomposition process is repeated until the desired sub-signals are obtained and filtered out ( or retained). Once the filtering is complete, the remaining sub-signals are added up to reconstruct the signal. </p> 

**In your project, what do you propose to improve the state of the art?**

<p style='text-align: justify;'>
A digital signal processing kit (DSP kit) is a specialized microprocessor with its hardware optimized to run signal processing algorithms. Most signal processing techniques are heavily reliant on floating-point operations, multiply and add operations, matrix multiplication operations, and convolution operations. Although it is possible for a general-purpose CPU to execute the above-mentioned operations, a DSP kit will do it in a much faster and energy-efficient way. This is because of the software and hardware level modifications that make the microprocessor especially suited to DSP. For example, to speed up the Fast Fourier Transform (FFT), one of the most important signal processing algorithms, a DSP kit may have multiple highly parallel multiply and accumulate (MAC) units, since the FFT heavily depends on multiply-accumulate performance. </p>

<p align="center">
  <img src="https://akulmalhotra.github.io/files/waveletecg/tikit.jpg?raw=true" alt="Photo" style="width: 400px;"/> 
</p>

<p style='text-align: center;'>
Figure 4: The TI TMS320C5515 eZdsp board </p>

<p style='text-align: justify;'>
To improve the state of the art in baseline wander removal, we implemented a wavelet-based filter on the TI TMS3320C5515 ezdsp kit. Figure 4 <a href="http://www.ti.com/tool/TMDX5515EZDSP">[2]</a> shows the top view of the DSP board. The original ECG signal had a frequency range of 0-64Hz, which was then decomposed by 7 levels to obtain the frequency band 0-0.5Hz, which contains the baseline wander. This band was then removed and the remaining bands were added to create the reconstructed signal. One thing that I would like to point out is that removing a particular band and then reconstructing the signal using wavelet-based filters can potentially ruin the output signal due to a phenomenon called aliasing. The good thing is that the aliasing is negligible at high levels of signal decomposition (like 7 in the baseline wander removal). Therefore, it does not affect the output signal in baseline wander removal. </p> 

**Please describe your results.**

<p style='text-align: justify;'>
Figure 5 shows the raw input signal with baseline wander, taken from the MIT-BIH Normal Sinus Rhythm Database <a href="https://www.physionet.org/content/nsrdb/1.0.0/">[3]</a>. The signal was passed through the wavelet-based filter as well as the traditional filters. Filtering was done both on the DSP kit and MATLAB for comparison and validation of the results. Figure 6 shows the output of the wavelet-based filter using the DSP kit. It can be seen that the baseline wander has been removed without impacting the desired components of the signal. The results of filtering with the traditional filters can be found in the paper. </p>

<p align="center">
  <img src="https://akulmalhotra.github.io/files/waveletecg/raw.jpg?raw=true" alt="Photo" style="width: 450px;"/> 
</p>

<p style='text-align: center;'>
Figure 5: Raw ECG signal </p>

<p align="center">
  <img src="https://akulmalhotra.github.io/files/waveletecg/filtered2.jpg?raw=true" alt="Photo" style="width: 450px;"/> 
</p>

<p style='text-align: center;'>
Figure 6: Filtered ECG signal using the wavelet-based filter </p>

<p style='text-align: justify;'>
<b>What are some papers/resources that you would recommend others to read so that they can get to know more about this field? </b></p>

<p style='text-align: justify;'>
To learn more technical details about this project, I would recommend reading <a href="https://ieeexplore.ieee.org/abstract/document/9073007">this paper</a>. I intentionally left out many details after wavelet-based filters (especially the decomposition and reconstruction processes) to keep this writeup concise. The interested reader can go through Robi Polikar’s <a href="http://users.rowan.edu/~polikar/WTtutorial.html">wavelet tutorial</a> for an introduction to wavelets,  the discrete wavelet transform, and multiresolution analysis. To learn more about the TI TMS320C5515 DSP kit, I would recommend <a href="https://www.eecs.umich.edu/courses/eecs452/Labs/Docs/C5515_DSP_System_guide.pdf">this guide</a>. To understand wavelet-based filtering better,  I would recommend <a href="https://ieeexplore.ieee.org/document/382009">this paper</a>. </p>

**What future work can be done in this area?**

<p style='text-align: justify;'>
This work focused on the implementation of one particular signal processing technique on the DSP kit to improve speed. In a similar manner, other signal processing algorithms can also be implemented on DSP kits for faster processing. Algorithm-hardware codesign is also an interesting future direction, in which signal processing algorithms can be designed for particular DSP kits. </p>


**References**

<p style='text-align: justify;'>
 [1] <a href="https://en.wikipedia.org/wiki/Electrocardiography">https://en.wikipedia.org/wiki/Electrocardiography</a> </p>
 
 <p style='text-align: justify;'>
 [2] <a href="http://www.ti.com/tool/TMDX5515EZDSP">http://www.ti.com/tool/TMDX5515EZDSP</a> </p>
 
 <p style='text-align: justify;'>
 [3] <a href="https://www.physionet.org/content/nsrdb/1.0.0/">https://www.physionet.org/content/nsrdb/1.0.0/</a>  </p>
