---
title: 'Tutorial on fMRI Test-Retest Reliability Estimation'
date: 2024-11-27
permalink: /posts/2024/11/fmri-test-retest/
tags:
  - FMRI
  - Test-retest
  - ROC
  - Mixed-Binomial Model
---

>This tutorial is based on my presentation at the [FMRI Lab](https://fmri.research.umich.edu/) meeting on November 26, 2024. You can find the pdf of the talk [here](https://yonglihe23.github.io/files/fMRI-GroupMtg-Nov26-2024-YongliHe.pdf).

In fMRI, we calculate statistic measures, e.g., t-, F-statstic, correlation coefficient, for each voxel to generate activation maps. Raw statistic maps are thresholded give labels to voxels with either active or inactive. In an ideal world, the classification of voxels into active/inactive would be invariant across different trials of the same task. In that case, the classification we yield from thresholding the statistic measure is the ground truth of activation. However, there is always variation of activation maps across different trials of experiment. This is due to, e.g., movement, physiological noise, ambient noise, and most importantly, the neural activity of the subject is not temporal shift invariant. Therefore, it is important to quantify the (test-retest) reliability of the activation maps we get from the acquired fMRI signals. 

One of the methods for this purpose is to calculate the [receiver operating characteristic (ROC)](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) curve. 

To get an ROC curve for a, say, t-score map, we sweep the threshold value, for each threshold, calculate (FPR,TPR), get a dot in the ROC curve. 
![roc]()
The definition of false positive rate (FPR) and true positive rate (TPR) are as follow: <br>
<center>$
 \text{FPR}=\frac{\text{FalsePositive}}{\text{FalsePositive+TrueNegative}}\triangleq p_I
$</center> <br>
<center>$
 \text{TPR}=\frac{\text{TruePositive}}{\text{FalseNegative+TruePositive}} \triangleq p_A
$</center>
Intuitively, you can view FPR and TPR as "false alarm" and "hit", respectively. 





