# FDA  Submission

**Your Name:**  Jamiu Ekundayo

**Name of your Device:**  cheXray

## Algorithm Description 

### 1. General Information

**Intended Use Statement:** This algorithm is intended for use in assisting a radiologist with pneumonia identification from chest x-rays.

**Indications for Use:** It is indicated for use in patients (male and female) within the age bracket 1-95 years with chest x-rays taken in the AP and PA view positions on a ER setting. Not indicated for use in patients.  

**Device Limitations:** The presence of edema, atelectasis and effusion  may reduce the performance of the algorithm in accurately predicting the presence of pneumonia in a chest x-ray. Conversely, the presence of infiltration and consolidation in the image may lead to improved performance of the algorithm at accurately predicting the presence of pneumonia from a chest x-ray.  

**Clinical Impact of Performance:** This algorithm's performance shows that it will be useful for screening chest x-rays for pneumonia and may also be used for workflow prioritization. 

### 2. Algorithm Design and Function

<< Insert Algorithm Flowchart >>
![flow_chat.png](attachment:flow_chat.png)

**DICOM Checking Steps:**

   1. Checked the dicom file to ensure the body part examined was chest
   2. Checked the dicom file to ensure the imaging modality was DX
   3. Checked the dicom file to ensure the view positions were AP and PA

**Preprocessing Steps:**

   1. Image standardization
   2. Image resizing 
   
**CNN Architecture:**
![my_model4_architecture.png](attachment:my_model4_architecture.png)

### 3. Algorithm Training

**Parameters:**

* Types of augmentation used during training - horizontal flip with 10% shift range in height, width, shear and zoom. Rotation range was set to 20 degrees.

* Batch size - 32 used for training; batch_size = length of validation dataset used for testing. 

* Optimizer learning rate - 0.0001

* Layers of pre-existing architecture that were frozen - All output layers except output layer 10 (block3_conv3)

* Layers of pre-existing architecture that were fine-tuned - output layer 10 (block3_conv3)

* Layers added to pre-existing architecture - dropouts and three fully connected layers 1024, 512 and 256

<< Insert algorithm training performance visualization >> 
![model4_performance_plots.png](attachment:model4_performance_plots.png)


<< Insert P-R curve >>
![model4_PR_plot.png](https://github.com/datasolver/Udacity_AI_for_Healthcare/blob/master/pneumonia_detection_my_submission/model4_PR_plot.png)

**Final Threshold and Explanation:** Final threshold = 0.387. This was the threshold that maximized F1_score (@ F1 score = 0.371). It corresponded to a 25% precision and 71% recall.

### 4. Databases
 (For the below, include visualizations as they are useful and relevant)

**Description of Training Dataset:** The training dataset is balanced for pneumonia and contains 2290 images sampled from 112,120 chest X-ray images with 15 (unique) disease labels from 30,805 unique patients.  

**Description of Validation Dataset:** The validation dataset is an imbalanced dataset containing 20% pneumonia cases and a total of 1430 images sampled from 112,120 chest X-ray images with 15 (unique) disease labels from 30,805 unique patients. 


### 5. Ground Truth

The labels were generated through text-mining radiologists' reports using a Natural Language Processing (NLP) algorithm. The 
NLP algorithm was reported to achieve over 90% accuracy. Moreover, this appraoch is fast and cost effective but it has inherent issues which might affect the accuracy of the algorithm and limit its clinical applications. For example, 
    1. the labels might not reflect the medical histories and/or blood test results of the patients
    2. possibility of image-label mismatch.


### 6. FDA Validation Plan

**Patient Population Description for FDA Validation Dataset:** 

The FDA validation dataset was acquired from six patients, all men with ages 58, 71 and each of the remaining four being 81 years old.

**Ground Truth Acquisition Methodology:**

The labels were generated through text-mining radiologists' reports using a Natural Language Processing (NLP) algorithm. The 
NLP algorithm was reported to achieve over 90% accuracy. Moreover, this appraoch is fast and cost effective but it has inherent issues which might affect the accuracy of the algorithm and limit its clinical applications. For example, 
    1. the labels might not reflect the medical histories and/or blood test results of the patients
    2. possibility of image-label mismatch.

**Algorithm Performance Standard:**

With AUC = 0.602 and maximum F1_score = 0.371, CheXray performs lower than CheXNet (Rajpurtar, et al., 2017). However, CheXray's F1 score is higher those of two radiologists (radioplogist 2 & radiologist 3) in Rajpurtar, et al. (2017).
