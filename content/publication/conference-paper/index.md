---
abstract: >-
  With the rising fluency and factual knowledge of large language models, many
  schools have banned ChatGPT from school networks and devices over concerns
  about students' potential cheating. In this project, we intend to investigate
  the ChatGPT model and propose a machine-generated text detector for the
  GPT-3.5 model. The project goal is composed of three parts: (1) explore
  statistical information of machine-generated text (word frequency, text
  length, or even sentence structure); (2) build the discriminator model on a
  mixture of machine-generated text and human-written text; (3) propose data
  augmentation methods to downstream tasks like Q\&A systems or text completion
  based on the analysis of the obtained discriminator and visualize the
  weights/attention.


  To reach our project goal, we construct a BERT-based classifier and an improved TF-IDF classifier to classify a given corpus into two classes: machine-generated text and human-written text. The model is first trained on the HC3 dataset and some similar datasets, which contains Q&A pairs both from human and machine. We then continuously fine-tune the dataset by taking out easily recognized patterns or words or statistical information. We hope by this data argumentation step, the dataset will be able to train more robust discriminators.
   
   As the discriminator model will learn the patterns of machine-generated text, it will be helpful for schools to identify those effortless work and appeal to parents to pay attention to their children's academic performance. As for the NLP community, all the tasks will contribute to understanding the machine-generated text and arouse ethical concerns about the power of AI.
slides: ""
url_pdf: "https://github.com/MGTD4ChatGPT/report/blob/main/Machine-Generated%20Text%20Detection%20for%20ChatGPT.pdf"
publication_types:
  - "4"
authors:
  - admin
  - Haoquan Zhou
  - Kexuan Huang
author_notes:
  - Equal contribution
  - Equal contribution
  - Equal contribution
publication: ""
summary: >-
  - Discriminated statistical information of machine-generated text to propose an explainable classifier, achieving comparable predictability to BERT-based models.

  - Performed a thorough analysis of data augmentations on response length, identifying that truncated sentences can decrease the model performance by around 5%
url_dataset: "https://github.com/MGTD4ChatGPT/Other"
url_project: "https://github.com/MGTD4ChatGPT"
publication_short: ""
url_source: "" 
url_video: ""
title: Machine-Generated Text Detection for ChatGPT
doi: ""
featured: true
tags:
  - Data Science
  - Deep Learning
projects: []
image:
  caption: ""
  focal_point: ""
  preview_only: false
date: 2023-04-21T00:00:00.000Z
url_slides: ""
publishDate: 2023-05-04T00:00:00.000Z
url_poster: ""
url_code: https://github.com/MGTD4ChatGPT/Experiment
---
