# 1   Introduction

Culinary herbs are primarily used to flavour or colour food and drinks. Each country cultivates and utilises its own unique selection, leading to a vast diversity of herbs. This project employs deep learning computer vision techniques to classify 20 common culinary herbs in Australia, addressing the challenge of identifying herbs that often have similar appearances.

The primary purpose of this project is to aid in the development of plant phenotypes. Phenotypes represent the observable characteristics or traits of an organism, influenced by both genetic makeup and environmental factors. Therefore, even the same herb species can exhibit totally different appearances when grown in varying conditions across different countries or environments. 

Additionally, this project supports the development of herbs for medicinal purposes, as culinary herbs can serve as dietary antioxidants. Identifying these herbs may provide valuable insights into their antioxidant properties.

### 1.1 Introduction Plan for Data Collection and Work Distribution

To collect the necessary plants, we held a group meeting and decided to produce our own images instead of using stock images to enhance the learning experience and practicality of our work. Consequently, we visited a garden centre and obtained 20 species of culinary herbs. Due to budget restrictions, we were only able to buy one plant per species. In order to still obtain a wide variety of images, we have created a specific image production plan, which includes different perspectives and zoom level. This can be found in section 1.2.

We then divided them into categories as follows: Keith and Chris handled 7 categories, while Ador was responsible for 6 categories. Each team member decided on its own for the choice of implemented models, which lead to a variety of models in our group. In the later phase of the project, we combined the individual produced datasets (20 categories) and captured new data under different conditions. 

### 1.2 Image Production 

For each herb category, a minimum of 50 images were captured from various perspectives to ensure a variety of images and a comprehensive representation. Specifically, 8 images were taken from each of the following views: side, elevated, elevated with zoom, and side with zoom. Additionally, 4 images were captured from a top view, and 15 images focused solely on single leaves. Figure 1 demonstrates the image variety of image production for this project. 

![image-20240629124921328](/Users/keith/Library/Application Support/typora-user-images/image-20240629124921328.png)

​										Figure 1: Image Production of Rosemary and Sorrel 

### 1.3 Herb Categories

The 20 herb categories of this project are shown in Figure 2. They are:

- Basil
- Catmint
- Catnip
- Chives
- Coral
- Cress
- Curry
- Fennel
- Lemon Grass
- Mint
- Mustard Greens
- Olive Herbs
- Oregano
- Parsley
- Rosemary
- Sage
- Sorrel
- Tarragon
- Thyme 
- Verbena

 ![image-20240629125134600](/Users/keith/Library/Application Support/typora-user-images/image-20240629125134600.png)

​								Figure 2: Images of 20 herb categories.

 

## 2   Evaluation of Individual Approaches

In this project five different models have been implemented. They are:

- MobileNetV2
- EfficientNetB4
- InceptionV3
- ResNet-50
- ResNet-152

### 2.1 Reasons for Selecting the Models

As described before the model selection was on an individual basis and independent of the selection of other group members. In the following the reasons for selecting the particular models are given:

**MobileNetV2:** 
 In phase 1, two research papers demonstrated that for fine-grained classification tasks on tea leaves, the MobileNetV2 was very powerful. The best performing fine-tuned MobileNetV2 model achieved 98% accuracy, while the second-best achieved 96%. These high accuracy results suggested that MobileNetV2 was an appropriate option for this project.

**EfficientNetB4:** 
 In comparison to MobileNetV2, EfficientNetB4 is a more advanced model with 19 million parameters, significantly more than MobileNetV2’s 3.4 million. Its complex structure may offer superior performance, making it a preferred choice for this project.

**InceptionV3:** 
 This model can capture features across different scales and utilises advanced factorisation techniques to streamline computational complexity without compromising performance, making it suitable for this project.

**ResNet-50:** 
 This model has the ability in capturing intricate patterns and features through its complex structure. Also, it incorporates residual connections to mitigate issues related to catastrophic forgetting in deep architecture. This model can be beneficial for this project.

**ResNet-152:** 
 Building on the capabilities of ResNet-50, the ResNet-152 model features a deeper architecture, potentially offering enhanced performance in extracting fine-grained details, which is why it has been selected for this project.

### 2.2 Training the Models

Overall, the datasets were trained with the 5 pretrained models, employing fine-tuning and data augmentation techniques. The dataset was divided into 60% for training set, 10% for validation set, and 30% for testing set. There is a major difference in the fine-tuning approach among the models. For MobileNetV2 and EfficientNetB4, only the last three layers (blocks) of the model were unfrozen and newly trained. In contrast, for InceptionV3, ResNet-50, and ResNet-152, all the parameters of the model were unfrozen and newly trained.

 

## 3   Results

The next step was to train and test the models with the extended dataset of 20 categories of herbs but without the new test dataset of different conditions. The model performances can be found in Figure 3:

![image-20240629125410842](/Users/keith/Library/Application Support/typora-user-images/image-20240629125410842.png)	

​										Figure 3: Model performances.

As a summary, the MobileNetV2 model obtained the highest accuracy, and the ResNet-152 model obtained the lowest accuracy. The MobileNetV2 model was therefore chosen for the rest of the project, with the following settings:

- Using pretrained model (final layer modified to fit number of classes)
- Early stopping mechanism (patience = 3)
- Learning rate: 0.01
- Step size: 8
- Gamma: 0.9
- Re-training last 3 layers (blocks)
- Optimizer: SGD
- Data Augmentation (Resize, CenterCrop, Normalize)

### 3.1 Testing MobileNetV2 Model on new Dataset with Different Conditions 

New testing images were collected under varying conditions, such as at dawn or night, to evaluate model performance. The original dataset was divided into training and validation sets, while this new collection served as the testing set. The original testing dataset remained unused. This approach tests the generalizability of the model, as the new dataset was not utilized during the training phase.

The accuracy of MobileNetV2 decreased from 98.7% to 80.20% with the new testing images. Despite this reduction, the model still demonstrated good generalizability. To improve the accuracy, multiple data augmentation techniques were implemented, which increased the accuracy slightly from 80.20% to 81.20%, which will be discussed in detail in section 4.

### 3.2 Classification Results

![Screenshot 2024-05-22 at 12.10.57 PM](/Users/keith/local documents/MQ/COMP8430/Group Project/Screenshot 2024-05-22 at 12.10.57 PM.png)

### 3.3 Interesting Findings About Classified and Misclassified Images

In general, the model is capable of effectively classifying all the herbs with only minor misclassifications, except for two categories. A major challenge arises in distinguishing between catnip and catmint.

 ![image-20240629125602069](/Users/keith/Library/Application Support/typora-user-images/image-20240629125602069.png)

​			Table 1: Results of Catnip being misclassified as Catmint

![image-20240629125633920](/Users/keith/Library/Application Support/typora-user-images/image-20240629125633920.png)

​									Figure 4: Images of Catnip (left) and Catmint (right)

As shown in Figure 4, the similar appearance between catnip and catmint makes it difficult to differentiate them, both for the model and the human eye. In Table 1, it displays the number of catnips misclassified as catmints before and after applying data augmentation techniques. In both cases, the model struggles to distinguish catnip and catmint effectively.

Another interesting finding emerged during the project, as depicted in Figure 5, which shows images of fennel taken in both early and later phases.

 ![image-20240629125651365](/Users/keith/Library/Application Support/typora-user-images/image-20240629125651365.png)

​			Figure 5: Image of Fennel taken in early phase 2 (left) and later phase 4 (right)

In the later phase 4, the fennel is obviously withered, with significant changes in colour and shape. Despite these changes, MobileNetV2 was still able to classify the fennel effectively and accurately. This demonstrates the model's capability to recognize objects with distinct changes in appearance, although it struggles with objects that have similar appearances.  

## 4   Improving the Model and Analysis

As the accuracy of the model decreased to 80.2% for the new testing dataset with more difficult conditions, we discussed in our group several possibilities to improve the model’s accuracy again. Our first idea was to use the testing dataset of the original dataset, which accounted for 30% of the dataset (or roughly 400 images), as additional data for the training and validation datasets. But since the dataset split was predefined by previous instructions, we decided against this procedure.

Since the new dataset with different conditions is basically showing the same plants that we just used in simple conditions before, we decided that fine-tuning the augmentation techniques would give us a good chance of increasing the model’s performance. Therefore, we individually tested the following augmentation techniques and compared the results which are shown in table 2.

 ![image-20240629125711041](/Users/keith/Library/Application Support/typora-user-images/image-20240629125711041.png)

​								Table 2: Augmentation techniques in comparison

Compared with the starting point without new augmentation techniques and an accuracy of 80.2%, the first 8 augmentation configurations performed either worse or just as good as this baseline. Therefore, we applied our knowledge about the new testing dataset in comparison to the original one. Since the plants did not change but the light conditions, we experimented with the ColorJitter augmentation technique and the fine-tuned hyperparameters (brightness = 0.3, contrast 0.4) resulted in an increase of the model’s performance to 81.22%. 

Although we were able to increase the performance of the model, we were not able to reach the same level of accuracy (98.74%) as the model had for the original testing dataset. In addition, with the pattern of misclassified images, discussed in section 3.2, we analyzed that augmentation was not able to compensate for the accuracy drop. Therefore, the reason for this drop has to be about the images itself and what the model did or did not learn during the training. The model was trained with images taken in ideal conditions to learn the features of the species. Exposed to the new dataset with more difficult conditions and the corresponding drop of accuracy, it can be concluded that the model was not robust enough to distinguish between some classes, especially when they have such similar leaf shapes like Catnip and Catmint.

 

## 5   Conclusion

In total, the MobileNetV2 model performance for phase 4 with 81.2% was good but not outstanding. The misclassification of the species Catnip and Catmint alone resulted in an 8% drop of accuracy, which did not occur in the original dataset. New data augmentation techniques were not able to accommodate the accuracy decrease. 

It is highly likely that the accuracy drop is linked to the small dataset with just around 1,300 images for 20 classes and very similar image production conditions. In addition, with only one plant per class, these are the major limitations. Also worth mentioning is that all code was only run once, which could lead to slightly imprecise accuracies compared to running the code several times and calculating the arithmetic mean. 

Potential improvements are to increase the number of images and use different plants for a higher variety per herb class. Furthermore, capturing fine grained details of leaf patterns, texture and shapes would strengthen the model’s robustness. Another potential improvement would be to include the new test dataset partly as the validation dataset when training the model.