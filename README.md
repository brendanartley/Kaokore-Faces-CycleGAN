# Kaokore-Faces-CycleGAN
CycleGAN model using real faces and faces from 16th-century Japanese paintings.

I have used multiple cycleGAN models converting landscape images into different artistic styles and wanted to used what I had learnt in these scenarios with datasets of my own. I ended up using a dataset of real faces scraped from Flickr.com, and I put together my own webscraped faces from 16th and 17th century japanese paintings.

With a CycleGAN you end up training two discriminators and two generators which are in a constant battle to lower their loss. Here is an example of the kaokore_face generator. It actually turned out quite well. After training this model for 100 epochs (4hrs on TPU's), I found that roughly 90% of the generated kaokore faces were quite good. The other 10% are ok, but they could be potentially improved by a longer training cycle, or improved model structure. 

## Example

![cycleGAN_example](https://github.com/brendanartley/Kaokore-Faces-CycleGAN/blob/main/CycleGan_example.png)


## Files

I have included the following files in the repository. To copy and run this code yourself please visit Kaggle Profile: https://www.kaggle.com/brendanartley to do so.





