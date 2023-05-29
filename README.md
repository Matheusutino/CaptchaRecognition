# Captcha Recognition using deep learning

This project was developed as the second project for the Computer Vision course in the Master's in Electrical and Computer Engineering (MEEC) program at the Faculty of Engineering of the University of Porto (FEUP). The objective is the recognition of captchas from an image using deep learning, specifically CNN, without using pre-trained or ready-made networks in pytorch.

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

## Objectives

In this way, our goal is to solve captchas using deep learning, specifically Convolutional Neural Networks (CNNs), which are robust models for object detection. During this process, the methods and ideas employed will be explained, as well as the analysis of the obtained results. Finally, the attempted methods that did not yield good results will be discussed, along with the limitations of the utilized method, and some ideas that may enhance the model's performance. Lastly, a conclusion regarding this challenge will be provided.

## Method used

### Label preprocessing

As we know the maximum size a captcha can have and the number of possible characters, we can transform the problem into a multilabel mode, which will have a dimensionality of max_captcha_len * num_characters_by_captcha. In this case, the problem arises from the inability to determine the exact length of the captcha. To address this, an additional character "$" was added, which symbolizes the absence of a character. In this case using the one-hot-enconder form.

### Generate dataset


In this part, as mentioned, the images are originally colored, but it doesn't impact the recognition of the captchas. Therefore, it was chosen to convert them to grayscale. Additionally, a transformation called RandomPerspective was applied to the training set to make the CNN more robust. In this case, the original training set was divided into two parts to also have a validation set, with a proportion of 95%/5%. In this case, three distinct dataloaders were generated: one for the "soft" captchas, another for the "hard" captchas, and also a combination of both. All of them had a batch size of 64 for the training set.

### Model

The model used was based on ResNet, specifically using the residual block as a reference, which has good robustness with skip connections. Other networks were tested, but the ResNet-based model performed the best.

## Results
