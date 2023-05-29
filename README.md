# Captcha Recognition using deep learning

This project was developed as the second project for the Computer Vision course in the Master's in Electrical and Computer Engineering (MEEC) program at the Faculty of Engineering of the University of Porto (FEUP). The objective is the recognition of captchas from an image using deep learning, specifically CNN in pytorch, without using pre-trained or ready-made networks.

## What is captcha?

Completely Automated Public Turing test to tell Computers and Humans Apart (CAPTCHA) is a commonly encountered online security measure designed to distinguish between human users and automated bots or malicious software. Captchas typically consist of distorted or obscured images, letters, numbers, or a combination of these, presented in a way that is difficult for automated programs to decipher accurately. 
The purpose of captchas is to prevent automated bots from abusing online services or attempting to gain unauthorized access. By requiring users to complete a captcha, websites and online platforms can verify that the interaction is being carried out by a human, thus ensuring security and protecting against spam, brute force attacks, and other forms of automated abuse.

## Understanding the difficulty of this challenger

For this challenge, two datasets were provided for captchas. The first one is referred to as "soft" and consists of simpler captchas, while the second one represents the "hard" dataset, which can contains more robust captchas with lines. In both cases, the captchas are composed of alphanumeric characters, including digits (0 to 9) and letters (a to z) abd can have 4 or 5 characters. Also contain some noise in the form of scattered dots throughout the image and has differents colors.

<p float="middle">
    <img src="images/soft - ck9g3.png" alt="Soft Captcha" width="350"/>
    <img src="images/hard - vtl5g.png" alt="Hard Captcha" width="350"/>
</p>

The first is a example of soft dataset where the label is ck9g3 and the second image is for hard dataset with label vtl5g. We can see that the second case is indeed more complex, to the point where even humans find it difficult to identify the first character.

The real challenge lies in correctly recognizing all the characters of the captcha, as a single incorrect character invalidates the captcha.

## Method used

### Label preprocessing

As we know the maximum size a captcha can have and the number of possible characters, we can transform the problem into a multilabel mode, which will have a dimensionality of max_captcha_len * num_characters_by_captcha. In this case, the problem arises from the inability to determine the exact length of the captcha. To address this, an additional character "$" was added, which symbolizes the absence of a character. In this case using the one-hot-enconder form.

### Generate dataset


In this part, as mentioned, the images are originally colored, but it doesn't impact the recognition of the captchas. Therefore, it was chosen to convert them to grayscale. Additionally, a transformation called RandomPerspective was applied to the training set to make the CNN more robust. In this case, the original training set was divided into two parts to also have a validation set, with a proportion of 95%/5%. In this case, three distinct dataloaders were generated: one for the "soft" captchas, another for the "hard" captchas, and also a combination of both. All of them had a batch size of 64 for the training set.

### Model

The model used was based on ResNet, specifically using the residual block as a reference, which has good robustness with skip connections. Other networks were tested, but the ResNet-based model performed the best.

## Results

In this case, we will initially analyze using only the original soft and hard datasets and then the combination of both.

Starting with the soft set, an overall accuracy of 0.843 was achieved and for each character, it was 0.962, which represents an acceptable rate given the difficulty of the task. While for the hard set, it was 0.835 and for each character, it was 0.959, slightly lower due to the greater difficulty of the captchas.

In all sets, it can be seen through the confusion matrix that the main challenge of the model is to distinguish the characters ('o' and '0'), ('l' and '1'), as they are really similar and their distinction is not so simple. This can also be noted by the lower precision, recall, and f1-score for these characters.

After that, I used the approach of combining the soft and hard datasets to have more training and validation instances and try to obtain a more robust model. The result was really surprising, where the overall accuracy was increased to 0.911 for soft and hard test datasets, representing a significant improvement. In addition, the accuracy for the characters was 0.959 for soft test dataset and 0.980 for hard test dataset.

It is noted that this is also a complex task because an error in a single character of the captcha already makes it incorrect. Therefore, the overall accuracy of the model will always be lower than the accuracy for the characters.

Thus, it is noted that with a larger number of data, the model can generalize better and capture the nuances of the problem. And the model was able to identify the number of digits in each captcha accurately.

For a better visualization of the data you can see the notebook.

## Limitations

The approach I used has a significant limitation since it does not work for a generic captcha of any size N. The model needs to know the maximum number of characters in the captcha.

Furthermore, even assuming that the maximum number of digits in the captcha is known, there would be a significant problem. For each additional digit added, there would be 37 more elements in the output vector, greatly increasing the dimensionality and consequently making it difficult for the network to converge.

## Conclusion

We noticed that the model has limitations, as described earlier, but for the proposed problem of captchas with 4 or 5 characters, the model performed satisfactorily. For better accuracy, the hyperparameters and network architecture could be explored further, as well as using pre-trained networks.

Additionally, we noticed that the main error of the network is in distinguishing the characters ("0", "o") and ("l" and "i"), as they are really similar. One approach would be to obtain more examples that use these characters to obtain a better and more robust model, which would likely greatly improve performance.
