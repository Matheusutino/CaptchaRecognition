# CaptchaRecognition

This project was developed as the second project for the Computer Vision course in the Master's in Electrical and Computer Engineering (MEEC) program at the Faculty of Engineering of the University of Porto (FEUP). The objective is the recognition of captchas from an image using deep learning, specifically CNN, without using pre-trained or ready-made networks.

## What is captcha?

Completely Automated Public Turing test to tell Computers and Humans Apart(Captcha) is a commonly encountered online security measure designed to distinguish between human users and automated bots or malicious software. Captchas typically consist of distorted or obscured images, letters, numbers, or a combination of these, presented in a way that is difficult for automated programs to decipher accurately. 
The purpose of captchas is to prevent automated bots from abusing online services or attempting to gain unauthorized access. By requiring users to complete a captcha, websites and online platforms can verify that the interaction is being carried out by a human, thus ensuring security and protecting against spam, brute force attacks, and other forms of automated abuse.

## Understanding the difficulty of this challenger

For this challenge, two datasets were provided for captchas. The first one is referred to as "soft" and consists of simpler captchas, while the second one represents the "hard" dataset, which contains more robust captchas with lines. In both cases, the captchas are composed of alphanumeric characters, including digits (0 to 9) and letters (a to z) abd can have 4 or 5 characters. Also contain some noise in the form of scattered dots throughout the image and has differents colors.

<p float="left">
    <img src="image1.jpg" alt="Soft Captcha" width="400"/>
    <img src="image2.jpg" alt="Hard Captcha" width="400"/>
</p>

The real challenge lies in correctly recognizing all the characters of the captcha, as a single incorrect character invalidates the captcha.

## Objectives

In this way, our goal is to solve captchas using deep learning, specifically Convolutional Neural Networks (CNNs), which are robust models for object detection. During this process, the methods and ideas employed will be explained, as well as the analysis of the obtained results. Finally, the attempted methods that did not yield good results will be discussed, along with the limitations of the utilized method, and some ideas that may enhance the model's performance. Lastly, a conclusion regarding this challenge will be provided.

##Results
