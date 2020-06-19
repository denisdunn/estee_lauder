# estee_lauder
Use Case: Performance analytics
Problem: Connecting performance analytics of assets out in the world(internet), to the original asset inside of a large database (1 million+) assets with little searching capability. The problem with embedded unique identifiers inside of assets, is that they are easily lost when go through the many different hands/companies on its way to social media. Using image classification we can circumvent that problem.

Objective: Build the foundation for image asset analytics & competitor analysis. Connect manipulated image assets found outside of the digital asset management system on social media and retail websites back to the filepath of the original asset inside of the digital asset management system. 

Hurdles: The training data for this project is inherently very small, there is only one picture per asset. We only know that the images are manipulated and not what is actually being done to the image,(cropping, superimposing,zooming etc). Some of the images are in close resemblance to each other. There is a fine line to walk to differentiate similar pictures, and to connect manipulated versions of same picture. 

Methods: 1) Image Classification 2) AutoEncoding
Image Classification:
Using Keras/Tensorflow, I took their imagedatagenerator and created synthetic versions of the originals. I used extreme unrealistic versions to help with overfitting. While using the imagedatagenerator, the neural network never sees the original picture, nor do I know what the external pictures (test images) are until testing. I tried many different neural network versions, and I found that my best models were shallow with a convolutional layer. I was constantly fighting overfitting due to a small proof of concept model of 44 images. Using Dropout layers, maxpooling, and finishing the model with an average pooling layer instead of dense layers connecting to the final dense layer. I found that average pooling helps with overfitting.

Dimensionality Reduction:
While visualizing the model using tensorboard projector for creative executives, I was able to summarize my model down to a small feature vector. I applied the feature vector to over 900+ images. Using different techniques including PCA, T-SNE, and UMAP, I further reduced the dimensions down to a 3-d projector. The groupings made a lot of sense,(products, campaigns, scenes). It was awesome to see how taking a 44 image classification model, and reducing dimentionality down to a small feature vector was still able to pull very meaningful information out of the images.

AutoEncoding: 
While working with feature vectors for visualization I dug into autoencoding, which can build replica images from very small feature vectors. I created a few autoencoders with the hope of building an even better grouping on the tensorboard projector. The groupings look very similar to the classification model vectors. On top of the visualization, I found two different ways to build my classifier using autoencoders.

1)I took the encoding part of the auto encoder froze the layers and trained the last layer as an image classifier with very good results. I would sometimes freeze and unfreeze layers, add dropouts, and tried stacking autoencoders. I built the classifier from different layer points, all with the goal of reducing overfitting.

2)Using a full autoencoder as a classifier. I am still working on the right loss functions and testing, but I am having success in using the autoencoder to try to redraw the picture I input into the model. The losses are dramatic when a picture is given that the model has never seen before. I think this could be a great solution to the problem. I am still testing how far to shrink the feature vector size for best results, and what loss functions are best to compare against. As one would think, if the autoencoder has seen the image it can redraw it with very little loss less than approx .06 mse. If the model has never seen a picture that is pretty random the loss is very high 16K mse. I am still testing the similar pictures to get a good idea of how best to use the autoencoder, but I see a very interesting use case for them. 

Visualization:
Here are some shots of the autoencoder. The top layer is the actual pictures, and the bottom layer are the autoencoded redrawn images, using a relatively small feature vector bottleneck. Also I attached a screenshot of the tensorboard projector.


![ScreenShot](https://github.com/denisdunn/estee_lauder/blob/master/image001.jpg)
![ScreenShot](https://github.com/denisdunn/estee_lauder/blob/master/projector_pic.JPG)
