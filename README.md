# Deep learning-driven pulmonary arteries and veins segmentation reveals demography-associated pulmonary vasculature anatomy
## Overview
This repository provides the method described in the paper:
“Deep learning-driven pulmonary arteries and veins segmentation reveals demography-associated pulmonary vasculature anatomy”

## Installation
```
conda create -n HiPaS python==3.10
pip install pydicom==2.4.4
conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
```

### Workflow
![image](https://github.com/Arturia-Pendragon-Iris/PuAV-Segmentation/blob/main/img/overview.jpg)

## Reproduce Our Follow-up Results
1) All CT scans are normalized from [-1000, 400] to [0, 1]. 
2) Prepare the chest segmentation for lung&heart, airway&blood vessels. Lesions and lung nodules can be also annotated if you want to get more accyrate reconstructed scans.
3) Prepare the reconstrution datasets with preprececc\datasets_RE.py. 
4) Run training_RE.py to train your datasets.
5) For segmentation, you can cut the arrayies into [128, 128, 128] cubes firstly or use the trainging structure shown in https://github.com/wolny/pytorch-3dunet.
6) Run training_seg.py to train your segmentation models.

## Supplementary Details
The voxel intensity of all scans was truncated within the Hounsfield Unit (HU) window of $[-1000, 400]$ and normalization to $[0, 1]$. For the super-resolution tasks, we grouped every five consecutive frames from 5.0 mm slice-thickness scans as an input patch $512\times512\times5$ in sliding windows, while the corresponding frame from 1.0 mm and the weights are concatenated together as the loss-term patch $512\times512\times10$. It was observed that this input size could capture the detailed tissue-level information for upsampling training. Similarly, due to the GPU memory limit, CT scans were cropped into sub-volume cubes of the size $128\times128\times128$ for segmentation tasks. We use PyTorch to implement the proposed method. The Adam optimizer was used for the segmentation network with an initial learning rate of $1\times10^{-4}$. The decay of the first-order momentum gradient is 0.9, and the decay of the second-order momentum gradient is 0.999.In the experiments, model training was executed on a Linux workstation with NVIDIA RTX A6000. Current parameters performed well for our tasks but are not necessarily optimum. Adjustment may be conducted in specific tasks.
