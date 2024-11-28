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
![roc](/images/roc_curves.png "ROC curves")
<center>**Figure 1: ROC curves**</center>

The definition of false positive rate (FPR) and true positive rate (TPR) are as follow: <br>
<center>$
 \text{FPR}=\frac{\text{FalsePositive}}{\text{FalsePositive+TrueNegative}}\triangleq p_I
$</center> <br>
<center>$
 \text{TPR}=\frac{\text{TruePositive}}{\text{FalseNegative+TruePositive}} \triangleq p_A
$</center>
Intuitively, you can view FPR and TPR as "false alarm" and "hit", respectively. 

>**Q**:Which one is better: guess all positive, or guess all negative? (suppose in fMRI, proportion of truly activated voxels is far less than 1/2)<br>
>**A**: They are the same! Guessing all positive will be the top-right corner in the ROC plot where as guessing all negative will be at the bottom-left corner. They corresponding to random classifiers with positive probability $\rho=1$ and $\rho=0$, respectively.

A natural question is: **how to know the ground truth activation classification?** If we don't have the ground truth, we can not calculate FP, FN, TP, TN. One straightforward solution may be taking a long scan, with many cycles of the same task, then take the resultant high reliability activation as ground truth. This method is simple but comes with high cost. An alternative way is to use statistic model to estimate the ground truth. Here we introduce a model proposed by [Genovese, et al.]( https://doi.org/10.1002/mrm.1910380319), which I call the **mixed-binomial model**.

The mixed-binomial model entails $M\geq 4$ repetitions of the same fMRI experiment. It contains the following major assumptions:
- The behavior of voxels across different trials is independent and identical distribution (i.i.d.);
- The behavior of each voxel is independent of other voxels;
- All voxels behave according to the same probability distribution.

These assumptions are obviously not true in real life. For example, given the clustering nature of activation voxels, the neighbors of a active voxel will have higher probability to be active, thus the second assumption is not true. However, the misfit these assumptions introduce should be negligible in most applications. Weaker assumptions could be made to better fit the reality, interested reader can refer to [the original paper](https://doi.org/10.1002/mrm.1910380319).

Now, let's introduce a few quantities that are essential for this model. The first one is called the *raw reliability map* $R_v$. It is defined as:
<center>$
 R_v=\text{Number of times out of M repetitions a voxel} v \text{is classified active}
$</center> <br>
Assume $R_v$ is drawn from a mixture of two binomial distributions:

(TBC)
---











