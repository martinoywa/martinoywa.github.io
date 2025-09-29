---
title: "MERA"
excerpt: "Music Emotion Recognition Algorithm for Music Recommendation" # <br/><img src='/images/histopathological-lung-cancer-architecture.png'>"
collection: portfolio
---
[https://github.com/martinoywa/MERA](https://github.com/martinoywa/MERA)

Music Emotion Recognition is a concept in Music Information Retrieval which hasn’t been around for a very long time, that is involved in determining or classifying emotions or mood that humans perceive in music using computer programs.

In this project I focused on the use of Deep Learning, a field in Artificial Intelligence that applies a concept called Deep Neural Networks (DNNs) for learning representations or patterns from data, which helps the networks performs their specified tasks such as classification of labels. Originally DNNs were only used in classification of images, but can now be used even on classification of text as part of Natural Language Processing (NLP), more specifically Natural Language Understanding. Both tasks will be used for emotion or mood recognition, later described in this project.

The project is further built on the concepts of Valence and Arousal in music, which represent negative to positive moods, and calm to energetic moods respectively. Both the audio and lyrics of a music are used since Arousal correlates well to audio while Valence correlates well to both audio and lyrics. The goal here is to use Deep Learning for classification of mel-spectrograms defined from music audio in image classification, and classification of music lyrics in text classification then averaging out the results to come up with a prediction of emotion. Two models will therefore be used in this project.