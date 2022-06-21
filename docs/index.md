# Malaria Detection

Using Deep Learning and Convolutional Neural Networks to creat a computer vision model to cost effectively detect maaria


By James Hochleutner

View code and files on Github
https://github.com/jhochle/MalariaDetection


- Malaria is a deadly disease that is transmitted by infected mosquitos.
- CDC estimates 400,000 people die of malaria annually.
- Traditional Malaria Detection requires examination of samples by trained labratory professionals
- Many types fo highly effective antimalaria medications are avaliable for treatment
- Low Cost, fast, and scalable detection could significantly reduce malaria mortality
- Using a computer vision model we can elliminate the need for a trained lab technician to evaluate samples
- Final model trained using a 14 layer Convolutional Neural Network (CNN) achieved 98.8% accuracy





[James Hochleutner Deep Learning Final Presentation.pptx](https://github.com/jhochle/MalariaDetection/files/8942084/James.Hochleutner.Deep.Learning.Final.Presentation.pptx)

## Data Set

Starting with a labeled data set of 27,558 color images takene from microscopic images of red blood cells

- All images are color (RGB) with color values between 0 and 255
- Images are all labeled as either "Parasitized" or 'Uninefected"
- Data is split into training (24,958) and testing (2,600) data sets
- Data sets are nearly perfectly balanced between Parasitized and Uninfected

## Data Pre-Processing

- Images are resized to ensure continuity when training the computer vision model
- First images are resized to 64x64 pixels for faster training times, and later 100x100 to test if lager image sizes improves accuracy
- I tested a number of image augmentation techniques to try to improve the model
- HSV, Gaussian Blurring, and ImageDataGenerator are all used to introduce more noise to the images and decrease model overfitting 
- Images are all normalized by dividing color values by 255 or 252 (HSV) 

![Blood_Samples](https://user-images.githubusercontent.com/62751735/174665229-fb97527f-c059-4e57-a932-1d74ac696912.jpg)


## Model Training Approach and Evaluation

- Models will all be trained using a common Random Seed
- Early stopping once valudation loss fails to improve in 2 Epochs will help to reduce model overfitting
- Models are evaluated on overall model accuracy and Recall to help minimize cases of failing to detect parasitized samples
- Plotting a Confusion Matrix hels with identifying the tradoffs between model accuracy and Recall

## Initial Model

- Base Model used is a Squential CNN with 1,058,786 trainable parameters
- The model will scan each image in small batches of pixels looking for common patterns
- Convolutional layers with ReLu activation functions are used
- Max Pooling Layers designed to extract the most dominant features
- Dropout layers randomly turn off filters to help prevent model overfitting
- This structure is repeated before adding a Flattening layer and a fully connected layer before a Softmax Activation layer
- Model performed extremely well with 98.3% accuracy

![image](https://user-images.githubusercontent.com/62751735/174659338-bc38317c-ca71-41d6-82b0-6755ed2c38e2.png)

![image](https://user-images.githubusercontent.com/62751735/174659505-28e1436e-b321-4fa1-9a2e-e791f092b8ee.png)

## Model revisions 

### Many attempts to improve model accuracy were taken 

- Adding additional layers to increase model complexity
- Changing Activation Function to Leaky ReLu
- Batch Noramlization Layers
- Image Augmentation (HSV, Gaussian Blurring, ImageDataGenerator, Larger Image sized)
- Changing Batch Sizes
- Kernal Regularization

None of these attempts significantly improved model performance

## Pre Trained Model Structure

Using the Pre Trained VGG-16 model yielded suboptimal results.  The VGG-16 model is more complex with over 19 layers and 14,714,688 trainable paramaters.  The VGG-16 model performed the worst of all models tested with 88.3% overall accuracy

## Simpler Model Structure

Since attempts to incrase model complexity from our base model failed to improve model performance and given that the far more complex VGG-16 model showed inferior performance, I decided to try to use a simpler model with fewer trainable parameters.  The approach worked and achieved superier overall accuracy and Recall

- Model with fewer layers (14)
- Far Fewer trainable parameters by reducing filters per layer (203,970)
- New loss minimizer
- Faster training speeds due to ferwer trainable parameters (20 seconds using GPU on GoogleColab Pro)
- Superier performance 98.8% overall model accuracy and 99% recall

## Final Model

![image](https://user-images.githubusercontent.com/62751735/174659306-e632fd28-3edc-4a42-8d3a-6e8a6675ed60.png)

![image](https://user-images.githubusercontent.com/62751735/174659455-ac4fe9c2-8efa-40b2-8aa2-e5f33d38d0f2.png)
