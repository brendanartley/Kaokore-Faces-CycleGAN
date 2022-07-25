# Kaokore Faces CycleGAN

This repository contains the code for a CycleGAN model that converts real faces into faces from 16th-century Japanese paintings. I did this using a dataset of faces from Flickr.com and faces from 16th and 17th-century Japanese paintings in the Kaokore Dataset.

Prior to this project, I had used these models to convert natural scenery into a painting style. This worked well, but I wanted to explore the limits of this model architecture. Initially, I tried working with sports balls (basketballs, soccer balls, baseballs, etc.), but these images were not similar enough to faces. As a result, the model would generate the same image regardless of the encoded feature representation. I also experimented with anime faces, but the same problem occurred.

In this project, I achieved the lowest average loss among the discriminators and generators after 100 epochs (4hrs on TPU's). This resulted in roughly ~80% of real faces being converted into passable 16th-century faces. The remaining ~20% were poor predictions with a lot of noise. This could potentially be improved by training for longer, increasing the model size, or using more training data. 

## Example

Here is an example of an output from the kaokore_face generator.

![cycleGAN_example](https://github.com/brendanartley/Kaokore-Faces-CycleGAN/blob/main/CycleGan_example.png)

## Files

[Model + Training](cyclegan-kaokore-faces-model.ipynb)

  This notebook contains the cycleGAN model. At the start of the notebook, all the necessary read and decode functions are defined for the TFrecord datasets. Then we define the model. The model consists of an encoder and decoder layer, the former having many upsample layers, and the latter having downsample layers. There are also model subclass instances with custom loss functions to evaluate the performance of the image discriminators and generators after each epoch
  
  In this version of the notebook, I provide the pre-trained weights after 100 epochs of training. This allows you to experiment with the model without having to train it. Feel free to copy and edit the notebook on [Kaggle](https://www.kaggle.com/code/brendanartley/cyclegan-kaokore-faces-model).

[Kaokore Japanese Faces Dataset](cyclegan-tfrecord-kaokore-faces.ipynb)

  This dataset took a little more work to collect than the human faces dataset. The images from this data source are from 16th and 17th-century faces from Japanese paintings. They are only accessible via HTTP, and I had to write a script to scrape these images. This notebook shows how I used urllib to mine these images and encode them into TFrecords. The resulting dataset contained 8000 kaokore faces with an image size of 256x256. Thank you to the National Institute of Japanese Literature for sharing this source.

[Human Faces Dataset](cyclegan-tfrecord-human-faces.ipynb)

  The human faces dataset was an easier source to collect. This was a dataset of 52,000 512x512 images on Kaggle which had been previously scraped from flickr.com. All I had to do was write a script to encode the pixels and image names as tf.data. Since the Kaokore faces are 256x256, all I did was resize the human faces in the model pipeline to this size. 

