# Computer Vision (CV) and Transfer Learning (TL) for Human Malaria Detection 

## Problem Statement

We hope to produce models that accurately identify malaria infection in human cells using computer vision to classify images as infected or clear. With this in mind, our question is: "How can machine learning algorithms be used to accurately identify malaria parasites in human cell images and classify them as infected or not to improve the efficiency and accuracy of malaria diagnosis?" 

## Motivation and Context

By creating a model that accurately and efficitenly does this, we hope to assist in improving quality of life and providing quick solutions for medical practictioners to accurately classify if human blood cells contain malaria. The Malaria Detection Project analyzes a dataset of cell images obtained from the NIH Website. The blood samples were collected from Chittagong Medical College Hospital in Bangladesh and subsequently photographed. By successfully creating this model, we are confident that we will be able to extract valuable insights from the data and contribute to the understanding of Malaria diagnosis and treatment.

## Data Description and Handling

Our data is distributed via Kaggle (https://www.kaggle.com/datasets/iarunava/cell-images-for-detecting-malaria) and originally sourced from NIH (https://lhncbc.nlm.nih.gov/LHC-research/LHC-projects/image-processing/malaria-screener.html). The blood samples were collected from Chittagong Medical College Hospital in Bangladesh and subsequently photographed. There are 27,558 cell images collected among 193 total patients (148 infected, 45 uninfected), sorted into two directories: parasitized and clear, with RGB coding. 

## Results

|   Model                           | Train Accuracy | Validation Accuracy | Test Accuracy |
|-----------------------------------|----------------|---------------------|---------------|
| Baseline CNN                      |      0.59      |         0.59        |     0.59      |
| Complex CNN                       |      0.96      |         0.95        |     0.95      |
| SOTA No Tune                      |      0.86      |         0.80        |     0.80      |
| Complex CNN Data Preprocessing    |      0.92      |         0.90        |     0.88      |
| Complex CNN Data Augmentation     |      0.95      |         0.91        |     0.93      |
| More Complex CNN Data Augmentation|      0.94      |         0.91        |     0.94      |
| ResNet Unfreezing Last 7 Layers   |      1.00      |         0.76        |     0.75      |
| ResNet Unfreezing Last 19 Layers  |      0.95      |         0.77        |     0.77      |

In the table above, we can see that the model with the highest test accuracy was the second model we tested (the Complex CNN), however it was closely followed by the More Complex CNN with Data augmentation and the CNN with Data Augmentation. The Complex CNN had a larger number of infected cells misclassified as uninfected but a lower number of uninfected cells misclassified as infected, whereas the Complex CNN with data augmentation had a larger number of uninfected cells misclassified as infected but a lower number of infected cells misclassified as uninfected. Since we care about reducing false positives, we could argue that Model 4 (Complex CNN with Data Augmentation) outperforms the rest, but an equally valid statement would be to argue that Model 1 (Complex CNN) outperforms the others due to the higher accuracy. 

## Conclusions and Inferences

**ResNet did worse than expected**

Some possible reasons:
- Ma, L., Shuai, R., Ran, X. et al. Combining DC-GAN with ResNet for blood cell image classification. Med Biol Eng Comput 58, 1251–1264 (2020). https://doi.org/10.1007/s11517-020-02163-3
    - This paper was using ResNet to look at simple images of White Blood Cells, which is similar in task and apperance to ours. In looking only to classify white blood cell images,their accuracy was 86.1%, and using initialized parameters accuracy increased only to 88.7%. We find similar performance behavior in our task, which leads us to believe simple images like cell specamines are not fit for such heavy machinery, and is overfitting.
- We *trained* the last few layers of the network, rather than *freezing* the first few layers and training the remainder. This could be a resonable next approach.

**Simple is better: ResNet not needed for simple images and task**

In some cases, it may be unnecessary to use a complex model like ResNet for simple images and tasks. While ResNet is a powerful architecture that has achieved state-of-the-art results in image classification, object detection, and other computer vision tasks, it may not always be the most efficient or effective choice like in our case. Even when improved, the ResNet model could not achieve the accuracy of the CNN models.

**Color and HSI are important features of microscopic samples when dye is involved**

Color and HSI (Hue, Saturation, Intensity) are critical features of microscopic samples when dye is involved. In microscopy, dyes are often used to enhance the contrast and visibility of microscopic samples, especially those that are difficult to see under normal illumination. Therefore, improving those characteristics helps our model.


## Future work
- Though ResNet did provide the best results, for which we suspect overfitting, it would be best to attempt fine-tuning with different learning rates to be sure.
- As mentioned, we could also attempt to freeze the first few layers and train the remainder, the complement of what we did in our actual attempt at improving ResNet's performance.
- Given Malaria is a parasitic disease with stages, clustering the infected cell images to uncover commonalities would allow us to better treat patients with urgency and or different doses of medication. A possible approach could be mixture models as they are a type of unsupervised machine learning algorithm that allows for the identification of underlying subpopulations or clusters.
 
