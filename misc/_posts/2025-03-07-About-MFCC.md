---
layout: post
title: "About MFCC"
date: 2025-03-07
categories: misc
tags: [misc, mfcc]
---

## Background

Based on psychoacoustics, the human ear's perception of frequency is not linear but rather closer to a logarithmic distribution. This means that the resolution of pitch perception is higher at lower frequencies and lower at higher frequencies. In simple terms, when a sound increases from 100 Hz to 200 Hz, people perceive a certain increase in pitch. However, if a sound increases from 2000 Hz to 2100 Hz—again a 100 Hz increase—the perceived pitch change is much smaller. At even higher frequencies, a 100 Hz increase might be barely noticeable. You can try this yourself [here](https://onlinetonegenerator.com/). 

This phenomenon occurs because our perception of pitch is not based on the absolute frequency values but rather on the "multiplicative" change. Going from 100 Hz to 200 Hz is a doubling of frequency, which feels much more significant than going from 2000 Hz to 2100 Hz, even though both changes are 100 Hz. The perceived change is much smaller when the frequency increase does not represent a large multiple of the original frequency. When analyzing speech or music, using a linear frequency scale to describe audio can dilute the **small differences in low frequencies** that are particularly important to the human ear, while exaggerating the **large differences in high frequencies** that are less perceptible to humans. To enable machines to **hear sound like humans**, the Mel scale was proposed, transforming the frequency axis into a shape more consistent with human auditory perception—finer resolution at low frequencies and coarser resolution at high frequencies. The resulting features (e.g., MFCC) therefore better reflect what we actually hear.

## Maths

1. **Pre-Emphasis**

Most audio signals in nature, including speech and music, have higher energy in the low-frequency range and lower energy in the high-frequency range. The main reasons for this phenomenon are as follows:

* **Human Voice:** The human vocal organs (vocal cords, resonance cavities) primarily generate low- and mid-frequency signals, while high-frequency signals are relatively weaker. An intuitive example is that vowels (a, e, i, o, u) are typically concentrated in the low-frequency range, whereas consonants (s, f, t, sh) contain more high-frequency components but are relatively weaker.

* **Sounds in Nature:** Many natural sound signals (such as wind noise and musical instrument sounds) experience greater absorption or scattering of high-frequency components during propagation, leading to lower energy in the high-frequency range.

* **Characteristics of Recording Equipment and Microphones:** The sensors in recording devices may exhibit significant attenuation in the high-frequency range, causing the recorded audio signal to have lower energy in the high-frequency region.

Since the high-frequency components have lower energy, audio processing tasks (such as speech recognition or music analysis) may struggle to capture features effectively due to the weak high-frequency signals. To address this, we often enhance the high-frequency components before feature extraction, typically using **a high-pass filter** for pre-emphasis:

2. **Framing**