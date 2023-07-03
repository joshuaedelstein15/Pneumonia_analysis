#### 07/03/2023
#### Joshua Edelstein



# Pnuemonia Analysis
## Overview
According to the World Health Organization (WHO), pneumonia kills around 2 million children under 5 years old every year and therefore is consistently estimated as the single leading cause of childhood mortality (Rudan et al., 2008). The WHO reports that 95% of new cases of pneumonia occur in developing countries, particularly in Southeast Asia and Africa. 
Bacterial and viral pathogens are the two leading causes of pneumonia (Mcluckie, 2009) yet require very different forms of management. Bacterial pneumonia requires urgent antibiotic treatment, while viral pneumonia is treated with supportive care. Therefore, accurate and timely diagnosis is imperative. A key part of the diagnosis is based on chest X-rays as they are routinely obtained and can help differentiate between the different types of pneumonia. However, the areas that struggle with childhoold pneumonia are lacking in doctors to interpret the xrays.<a name="cite_ref-1"></a>[<sup>[1]</sup>](#cite_note-1)

[^1]: [Data from Cell.com](https://www.cell.com/cell/fulltext/S0092-8674(18)30154-5)

## Business Understanding 
Given the issue at hand, there are 2 possible approaches. The first is to have many qualified doctors on hand in these countries to read all the xrays that are coming in and suggest a course of treatment. However, being that there are so many xrays this can be extremely time consuming, costly, and we may not have the requisite amount of doctors vonlunteering to go. 
Instead a leading doctor on the ground in Africa, Dr. Xavier Radiance, suggested creating a model that identifies whether a patient has pneumonia in general or not. If the model makes a positive prediction for pneumonia the xray will be passed over to a doctor to read whether the patient indeed has pneumonia and if they do, whether it is bacterial or viral. This method will cut down on the number of doctors required as they no longer have to read all the xrays; rather only the xrays that have been predicted positive. Our goal is to create the model for use by the doctors in these countries.
It's important to think about whether false positives or false negatives are worse in this case. A false positive means that the model predicts that the xray has pneumonia when it really doesn't. This may lead to providing treatment for a patient when it is not necessary. While a false negative means that the model predicts that the patient doesn't have pneumonia when he really does. This would mean not giving a patient treatment when they do need it. Being that we have a safety net of doctors reading the positive xrays, we don't need to be concerned for false positives nearly as much as false negatives, as the doctors will read all the xrays that are predicted positive. As such we will want to have a recall as high as possible so we catch all the patients with pneumonia.

<div>
<img src="images/xray.jpg", width = 900, height = 450/>
</div>

Photo by <a href="https://unsplash.com/@nci?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">National Cancer Institute</a> on <a href="https://unsplash.com/s/photos/x-ray?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  

## Data Understanding and Preprocessing
Content
This public dataset of 5,863 X-Ray images is provided by Mendeley data. The dataset is organized into 3 folders (train, test, val) and contains subfolders for each image category (Pneumonia/Normal). The  pneumonia are a labeled mix of bacterial or viral. 

The X-ray images were taken in 2017 from cohorts of pediatric patients between one to five years old from the Guangzhou Women and Children’s Medical Center, Guangzhou. All chest xrays were initially screened for quality control by removing all low quality or unreadable scans. The diagnoses for the images were then graded by three expert physicians.<a name="cite_ref-1"></a>[<sup>[2]</sup>](#cite_note-2)


[^2]: [Data from Mendeley Data](https://data.mendeley.com/datasets/rscbjbr9sj/2)


We began by performing some basic EDA.

We found that we had 3 datasets: Train, Test, Val. We used filepaths to load up the dataframes with their corresponding labels. The train set had 5216 chest xrays, test had 624 test xrays, and val had 16. Being that the validation set was so small, we decided to create a new validation set using a `train_test_split` on the train set. This resulted in new train that had 4277 xrays and a new val that had 939 xrays. 

Here is the breakdown of xrays with pneumonia in all 3 sets:

<div>
<img src="images/train_dist.jpg", width = 400, height = 300/>
</div>


<div>
<img src="images/val_dist.jpg", width = 400, height = 300/>
</div>

<div>
<img src="images/test_dist.jpg", width = 400, height = 300/>
</div>

And here is a summary of the above: 

<div>
<img src="images/summary_dist.jpg", width = 300, height = 100/>
</div>

We also pulled up sample images from the train set, of Pneumonia and Normal patients.

<div>
<img src="images/normal_xray.jpg", width = 800, height = 400/>
</div>

<div>
<img src="images/pneumonia_xray.jpg", width = 800, height = 400/>
</div>

## Modeling 

### Baseline Model
For our baseline model we created a very simple model. We loaded up the data with `ImageDataGenerator()` and `flow_from_directory()`. We then reshaped the images and labels, to make sure the model would run properly. Finally, we created our model as a sequential model, where one layer would build on the next. It had a Dense input layer with 64 units and used `'relu'` activation, and a Dense output layer with `'sigmoid`' activation and one output. We then compiled the model with a `'SGD'` optimizer, loss of `'binary crossentropy'` and accuracy as our metric. We then created an `early stopping` parameter for our model if the results were not improving after 5 epochs. As mentioned earlier, being that the most important metric for us is recall, we monitored the models loss in the stop parameter, as the better the model the lower the recall.

Here is how our model scored on the testing set:

<div>
<img src="images/baseline_report.jpg", width = 300, height = 133/>
</div>

talk about how it predicts everything as pneumonia. Then do final model. explain it well from cnn to skip step. then ...



