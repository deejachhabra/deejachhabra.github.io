---
title:  "Multi Class Image Classifier"
mathjax: true
layout: post
categories: 
          -github
          -website
---
Problem Statement:

We have three image dataset consisting of 3 classes, Motorbike Images( 798 images), Airplane Images ( 800 images ), Schooner Images ( 63 images ). 
![top](https://user-images.githubusercontent.com/108027722/207745815-895f3d82-4f35-4bec-afea-f4e2b016183c.png)
						Photo by The Click Reader

Approach:

We will use Convolutional Neural Network for Image Classification as it is the best model for Image datasets as it has neurons that learn weights and Kernels to apply convolutions. So if we have less files for a particular Image in our dataset like in this one, we can apply convolutions to increase the dataset size like horizontal flip, vertical flip, zooming image, rotating it etc.


As we do not have enough images for the datasets, we will use Image Data Generator which will help us in generating many images based on the parameters passed like Rotation, Zoom, Flip etc. We will pass the image data generator to our model. And we will take a look at how our model performs then.


I'll explain the three models below but before that let us discuss label encoder. We do not have labels in our dataset. So, we use label encoder to generate labels based on our dataset. As we have 3 classes, we pass 3 in our model so that our labels are encoded as (0,1,2)


An example of training data Image:

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/1.png)

These are just Airplane Images. One Image per dataset is in the Colab notebook. But as we can see that the images do not have labels, we have just the images.


Image Data Generator: 

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/2.png)

As discussed earlier there are many parameters to pass. I've picked these amongst them. This will help us to create additional data images based on parameters passed.


Every Model is trained on 10 epochs


Model 1:

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/3.png)

Model 1 consists of 4 convolution layers, filters ( number of neurons = 16) a kernel size of 5*5, padding (same), activation function 'relu', and input_shape=(150,150,3).input_shape is passed only to the first layer to define the dimensions of input.  it is passed 150,150,3 because of colour image(RGB channel) else we would have passed (150,150). In the end we pass one 'Flatten' layer to flatten out output received from the immediate MaxPooling Layer. We add a Dense Layer ( this is not a convolutional layer ) which has 512 neurons in it. After this an Activation 'Relu' is passed. The last layer in our model is the Dense layer with 3 neurons, because we want our output 3 classes and an activation of softmax which defines probablities between 0 and 1. So what is happening in the last layer is that outputs of 3  neurons is getting converted into 3 probabilities which lie between 0 and 1. For example: lets say it is [0.3,0.4,0.3] . So our class 1 is most predictable than others.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/4.png)

Our Accuracy and Loss for Model 1 seems a bit linear. May be because epoch size is 10.
![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/5.png)
Let's see if we can improve it further.

Model 2:

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/6.png)

So we are tuning hyperparameters now. This model has 32 instead of 16 neurons per layer. Additionally, we change the kernel size from 5*5 to 3*3. Rest everything is self explanatory as it is almost same from the model 1.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/7.png)

Let us plot out loss and accuracies.

![wget](https://github.com/deejachhabra/deejachhabra.github.io/raw/master/_posts/8.png)

Compared to our Model 1 , where there were drastic peaks in the data. This is a little smoother. Is that because of the kernel size we chose? 








Model 3:






We kind of changed our neural network architecture a bit in this one. Instead of keeping the same number of neurons, we have kept neurons in increasing order(32, 64, 128, 256). Rest everything is same as our previous models.




Does it look more smoother than the previous one?

YES. It is more smoother because we increased the number of neurons.








LETS TRY DECREASING THE NUMBER OF LAYERS AND SEE THE PERFORMANCE

Model 4:



So this time our model only has 3 layers. 




Let's see what is our training and validation loss and accuracies.




Not much improvement.

Lets decrease the number of layers to two this time and check.








Model 5:


So, now we only have 2 layers with 8 neurons per layer.  I've also changed the learning rate from 0.001 to 0.01 in this.


Accuracy:


Lets see what is our validation and training loss and accuracies.





Even with 2 convolutional layers our model is performing very well. 

Validation loss is very low. 

What might be the reason for that?







Model 6:

Let us try one more model with just 1 layer. Let's see can we achieve the accuracy similar to the above model. Learning rate is again 0.001.


Our model has just one layer. 



Lets see our Loss.



Even with so many jumps while training our model performs well on validation set.











Our model fits perfectly with our data. 

Lets plot the model accuracies.



Let plot all model's accuracies together and check which performs better.




As is clearly visible, Model 5  And as stated previously this is because our model fits very well to our dataset. 

The highest accuracy is of Model 3 [98 %]


Improvement:

Referred multiple sources to generate 6 different models. I have taken reference just for basic tasks such as uploading data, creating directory, making [X,y] - Training and Test Dataset, loading layers, activations etc.

Tried to tune various hyper parameters to achieve model accuracy till 96%. 

Tried adding an Image Data Generator to generate transformations of images so that my model can learn better.


References:


https://www.analyticsvidhya.com/blog/2021/06/how-to-load-kaggle-datasets-directly-into-google-colab/    


https://www.kaggle.com/code/rajmehra03/flower-recognition-cnn-keras


https://www.youtube.com/watch?v=j-3vuBynnOE&t=192s   

https://blog.keras.io/building-powerful-image-classification-models-using-very-little-data.html  


https://www.geeksforgeeks.org/keras-fit-and-keras-fit_generator/   


https://keras.io/api/preprocessing/image/          


https://neptune.ai/blog/google-colab-dealing-with-files   


https://matplotlib.org/stable/gallery/lines_bars_and_markers/barchart.html  


https://www.geeksforgeeks.org/adding-value-labels-on-a-matplotlib-bar-chart/          


https://www.youtube.com/watch?v=9pDlJ5aAFN4         
