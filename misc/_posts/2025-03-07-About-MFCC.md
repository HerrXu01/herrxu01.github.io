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

### Pre-Emphasis