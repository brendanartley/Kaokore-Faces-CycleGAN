# Kaokore-Faces-CycleGAN
CycleGAN model using real faces and faces from 16th-century Japanese paintings.

I have used multiple cycleGAN models converting landscape images into different artistic styles and wanted to used what I had learnt in these scenarios with datasets of my own. I ended up using a dataset of real faces scraped from Flickr.com, and I put together my own webscraped faces from 16th and 17th century japanese paintings.

With a CycleGAN you end up training two discriminators and two generators which are in a constant battle to lower their loss. Here is an example of the kaokore_face generator. It actually turned out quite well. 

After training this model for 100 epochs (4hrs on TPU's), I found that roughly 90% of the generated kaokore faces were quite good. The other 10% are ok, but they could be potentially improved by a longer training cycle, or improved model structure. 

I was reading about the improvenments of StyleGAN model which generates real faces, and they recently made huge improvenments in their model working on filitering out background noise. This is something I should look into in order to generate a higher percentage of accurate kaokore faces. 

## Example

![cycleGAN_example](https://github.com/brendanartley/Kaokore-Faces-CycleGAN/blob/main/CycleGan_example.png)


## Files

[Model + Training](cyclegan-kaokore-faces-model.ipynb)

  This notebook contains the bulk of the work done to create the cycleGAN model. At the start of the notebook, all the necessary read and decode functions are defined for the TFrecord datasets. Then comes defining the model. Upsample and Downsample layers are created which make up a good portion of the discriminators and generators that are going to be part of the network. I also define a model subclass with custom loss functions to evaluate the effectiveness of the image discriminators and generators.
  
  In the notebook script I provided here on Github, I use pre-trained-weights from 100 epochs of training. This line can easily be commented out and the model can be trained from scratch. Feel free to copy and edit the notebook on Kaggle.

[Kaokore Japanese Faces Dataset](cyclegan-tfrecord-kaokore-faces.ipynb)

  This dataset took a little more work to create than the human faces dataset. When I started out with this project I was looking for some sort of artificial face dataset to use in a cylceGAN model. I originally trained the model with anime faces, but the images were far too small for the model to learn any notable features. I finally found this data which had been collected by the National Institute of Japanese Literature of 16th and 17th-century faces from Japanese paintings.

  I used urllib to scrape these images from their website and encoded them into TFrecords. This is a dataset of 8000 kaokore faces with an image size of 256x256 which I made available to all users on Kaggle. 

[Human Faces Dataset](cyclegan-tfrecord-human-faces.ipynb)

  The human faces dataset was a little easier to create. This was a dataset of 52,000 512x512 images on Kaggle which had been previously scraped from flickr.com. All I had to do was write a script to encode the pixels and image_name as tf.data. Since the Kaokore faces are 256x256, all I did was resize the human faces in the model pipeline to this size. 
  
 ## Note
 
 To copy and run these code files yourself please visit [Kaggle](https://www.kaggle.com/brendanartley) and fork and edit any notebook you would like!






