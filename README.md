# Progetto-NL2-Gleason-Challenge-2019
Project for NecstCamp NL2: Automatic Gleason Grading

Credits to:
- Luca Pagano
- Ernesto Natuzzi
- Daniele Kota Russica

For a more documentated explanation, check report.pdf

## Abstract
Prostate Cancer (PCa) is the sixth most common and second dead- liest cancer among men worldwide. The aggressiveness of prostate can- cer is measured by Gleason grading, a system based on the appearance of cancer cells. It is usually performed via visual inspection (with a microscope) of the prostate tissue by expert pathologists. However, this is a time-consuming task and suffers from very high inter-observer variability. Automatic computer-aided methods have the potential for improving the speed, accuracy, and reproducibility of the results. This challenge aims at the automatic Gleason grading of prostate cancer from H&E-stained histopathology images through the use of a neural network, performing multiclass semantic segmentation.

## Dataset
- 244 patients with six respective labels
- 96 patients without labels

For the training we split the 244 patients in a training dataset and a validation dataset, following the 80-20 convention

## Our Approach
Each patient has from 3 to 6 label, each annotated by an expert pathologist, with 6 pixel values (0 for background, 1-5 for Gleason Grading). 
Firstly, we decided to combine them through the STAPLE algorithm, in order to have a single label per image that should best represent the tumour grading.
![ComparisonStaple](https://github.com/Lp1807/Progetto-NL2-Gleason-Challenge-2019/assets/93043012/d70cbebe-1136-4fa1-b6ff-65c1df04442a)


We decided for hardware reason to resize the image from 5120x5120 (on average) to 1024x1024 and divide them into patches of 512x512 with 50% overlapping, for a total of 9 patches per image.
<img width="1064" alt="toPatches" src="https://github.com/Lp1807/Progetto-NL2-Gleason-Challenge-2019/assets/93043012/13a7ee26-3f11-4e17-9791-7ab09c26d48a">
<img width="1063" alt="overlapping" src="https://github.com/Lp1807/Progetto-NL2-Gleason-Challenge-2019/assets/93043012/b08fa878-62e3-4aaa-a714-98f238dddc1c">

For the training we used a UNet with an EfficientNetB4 as the backbone; we used data augmentation for our 244 patients, in order to improve the accuracy of the model and avoid overfitting.

To implement the proposed solution and train the proposed DL model, we use Colab Free, which offers a NVIDIA T4 GPU with 12 GB RAM. 
The model was implemented in Keras (version 2.12.0), extended with Segmentation Model (version 1.0.1), for the evaluation metrics and training losses.


## Results

<img width="1147" alt="Screenshot 2023-09-21 alle 21 17 10" src="https://github.com/Lp1807/Progetto-NL2-Gleason-Challenge-2019/assets/93043012/b299ae7e-6db1-4fee-8b6d-faea42cebd82">


