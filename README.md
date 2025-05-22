# HSF Segmentation by MedSegMamba
This repository contains the implementation of **MedSegMamba**, a hybrid 3D CNN-Mamba deep learning model for **hippocampal subfield (HSF) segmentation** from T1-weighted MRI scans.

## Project Overview

Traditional segmentation tools like FreeSurfer, while popular, suffer from long runtimes and limited accuracy in small substructures. MedSegMamba addresses these limitations by combining the **local feature extraction capabilities of CNNs** with the **global sequence modeling of the Mamba architecture**.

This project focuses on the segmentation of **13 hippocampal subfields**, trained and evaluated on **1,226 T1-weighted MRI scans** from diverse neuroimaging datasets.

## Key Features

- Hybrid CNN + Mamba architecture
- Patch-based 3D segmentation using 96×96×96 cubes
- Selective Scan and Visual State-Space modules for efficient long-range spatial modeling
- Custom loss function: `0.4 * Dice Loss + 0.6 * Class-Weighted NLLLoss`
- Trained and evaluated on 7 public datasets:
  - ADNI, AIBL, BGSP, IXI, OASIS-1, OASIS-2, NIFD

All images were resampled to **1mm³ resolution**, skull-stripped, and intensity-normalized. Ground truths were generated with FreeSurfer.

## Model Architecture

- **Encoder-decoder structure** with skip connections
- **VSS3D (Visual State-Space 3D)** blocks leveraging SS3D scanning across 48 orientations
- **13-class output** for non-lateralized hippocampal regions
- **Softmax** over final voxel-wise predictions

## Training Details

- Batch size: 1
- Patch size: 96×96×96
- Epochs: 30 (due to resource constraints)
- Optimizer: AdamW, learning rate = 1e-4
- GPU: NVIDIA T4 (15GB)
