---
title: "Automatic Recognition of Simple Sentences in British Sign Language using Computer Vision and Machine Learning"
excerpt: "My 3rd Year Dissertation using Recurrent Neural Networks to accurately translate a range of dynamic signs in BSL<br/><img src='/images/BSL-Cover.png'>"
collection: portfolio
---
Grade Achieved: 1st

## Abstract

Gesture recognition is a broadly researched aspect of computer vision; however, there are a limited number of works which apply it to the interpretation of British Sign Language (BSL), and in particular dynamic signs. This work explores the challenges involved in real-time sign recognition, utilising a Recurrent Neural Network (RNN) with Long Short-Term Memory (LSTM) cells to capture temporal information to aid classification. The MediaPipe library is utilised in order to create a system which is signer-independent by extracting hand landmarks from each frame of a video. We primarily explore the impact of various data pre-processing steps, and analyse common causes of confusion between signs. Although the model proposed in this work achieves only 55.7% accuracy on 6 words, the results are promising for future work.

## Perspective
Having been with my Deaf partner since 2016, this project was close to my heart, and something I had been itching to tackle for years. Automated sign language recognition is a variation of automated gesture recognition, but without the benefit of being designed to be easy for computers to recognise. Additionally, much research into the field focuses on American Sign Language - whose signs are often more static than the BSL counterparts - or on the alphabet, which are some of the simplest signs available. I instead chose to use this project to explore how temporal information could be utilised by recurrent neural networks to effectively translate dynamic signs in real time with as little bias to the user as possible. 

## Summary
Although the focus of the project was initially on the machine learning architecture, much of my time was spent instead on data analysis and cleansing. Extensive BSL datasets are difficult to find and time-consuming to create, so I used [BOBSL](https://www.robots.ox.ac.uk/~vgg/data/bobsl/), an annotated collection of BBC signing videos. Unfortunately, I found that the time-stamps for each sign were not specific enough, resulting in much of the subset I had gathered being largely useless. This was a costly mistake on my part, as I then had to spend a significant amount of time cleaning my dataset, but a fantastic learning opportunity. Once I had verified the data I had gathered to be clean, I was able to explore the impact of varying the words, the number of samples the model was trained on, and the number of frames in each sample.

The model used was relatively simple, with four LSTM layers and 3 dense layers. This design was adapted from [an existing paper](https://www.mdpi.com/2079-9292/11/19/3228) which proposed significantly better results than I was able to replicate. This architecture is seen below.

<img src="/images/BSL/model_plot_original.png" style="display:block; margin: 0 auto;" />

Instead of using feeding the raw images into the model, we use hand landmarks extracted using [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker). This drastically reduces the computation required and allows the RNN to be completely independent to features such as skin colour, room brightness and camera quality, assuming the MediaPipe library outputs the correct data. 

<img src="/images/BSL/Hand Detection.png" style="display:block; margin: 0 auto;" />

The results, as previously mentioned, are underwhelming, but promising for future work. The accuracy in each test can be seen below. I found that the most common cause of error was either bad input data or signs which are somewhat similar to each other.

|                   **Model**                   | **Accuracy** |                          **Qualitative Comments**                         |
|:---------------------------------------------:|:------------:|:-------------------------------------------------------------------------:|
|                    4 Words                    |      52%     |                                Unremarkable                               |
|                    6 Words                    |      36%     |                            Many false positives                           |
|               6 Words - Cleaned               |     50.8%    | Improved recognition of signs, false positives filtered by non-sign class |
|         6 Words - Verified, 24 Frames         |     55.7%    |          Confusing in similar signs, very good for distinct signs         |
|        6 Words - Unverified, 24 Frames        |     45.2%    |                    Many false positives from non-signs                    |
| 6 Words - Verified, 24 Frames, With Pose Data |     44.4%    |                      Untested - likely high confusion                     |

A brief demonstration of the project outcome can be seen in the video below, in which the short sentence "Hello, do you want some food?" is successfully translated.
<video width="75%" controls muted style="display:block; margin: 0 auto;">
    <source src="/files/BSL-demo.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>


## Full Paper
My full dissertation submission (sans code or data) can be viewed here.
<object
  data="/files/BSL-project.pdf"
  type="application/pdf"
  width="100%"
  title="Embedded PDF Viewer"
>
  <p>
    Your browser does not support PDFs. [Download my dissertation PDF](/files/BSL-project.pdf)
  </p>
</object>

<br>

If you have any questions about this or my other work, feel free to send me an email!
