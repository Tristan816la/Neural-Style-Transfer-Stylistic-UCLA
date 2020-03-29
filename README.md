# Neural-Style-Transfer-Stylistic-UCLA

(Notice: This readme is about my insights on how to implement neural style transfer. If you have already known the key steps for implementing this model, it's not necessary for you read this readme but go directly using the model.

This model uses tensorflow 2.
)

This is a project about neural style transfer. Like other AI projects, an useful model (VGG-19) is provided by someone else and what I did was to implement and optimize this model. Though there are other methods that could simply achieve the style-transfer effect, like using TF-Hub, I found it helpful to truly implement the VGG-19 model because users of this model could tune the hyperparameters to personalize their images.

Tensorflow offers a really good tutorial on neural style transfer, and this project is made based on the content they shared in their tutorial:
(check their link): https://www.tensorflow.org/tutorials/generative/style_transfer

There actually are a lot of other tutorials on neural style transfer and how to use the VGG-19 model, but what they usually don't mention is how to tune the hyperparameters, how to use this model, and the math and CS insights behind this model. What I would like to share next was the logic behind my code, and the experience I got from experimenting my code.

## 1. Hyperparameters
1) Content layers & Style layers:
For a neural network, the rudimentary layers are used for detecting small features like an small edge of an object and some small color points. So, we usually only choose the later layers that has the big picture of the image and from which we would know what was on the image. 

For content layer, I recommend using 'block5_conv2' or 'block5_conv3'. And I usually don't tune style layers. By implementing the "load VGG-19" model section, you would see a prediction based on the layer you choose, which includes the top-5 probabilities of the item in your image. If you find it truly accurate, you can then change the content layer to make it do a better prediction.

2) Style-weight and Content-weight:
These are used to tune the proportion of the effects of your content or style images on your synthesized image. Usually the style weight is at e-2 range, and the content weight is at e4 range

3) Epochs & steps per epoch:
More epochs would take more time to train this model but could help achieve a deeper effect. Usually 100 epochs would take 6-7 seconds by using colab GPU.

4) Total Variation Weight:
This is the hyperparameter to reduce the noisy effect on your synthesized picture. It is used to achieve a regularization effect. (For content image with more color variation, I recommend increase this weight)

## 2. VGG-19 Model
(For doing neural style transfer, It is convention for people to use VGG-19 instead of VGG-16, which are used more widely.)
The analysis of the VGG-19 model and how it works is beyond the scope for practical purposes, so in the folder I include the paper of this model's author as reference.

For optimizing the model, I used the adam optimizer. Adam optimizer stands for adaptive moment estimation, and it is a decent optimizer for doing image processing, image classification, and of course, neural style transfer.

## 3. Process the images
There is no need to pre-process the image, as I included the load_img function that could help with resizing and transferring the image into a tensor. However, it is recommended for users to deal with the noisy part of the images (e.g. a dark tree in a really bright garden) so that neural style transfer would achieve a better effect.

For choosing images, I recommend using images with less variation in color, for both style and content images to achieve a better effect. 

## 4. Synthesized images
Some samples of synthesized images are already in the folder-- "transferred images", and you could definitely check them to see if you came up with better insights to train this model and do hyperparameter tuning.
