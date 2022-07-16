# Image-Caption-generator
### Summary:
The objective Of this project is get hands on generating captions to the image or images that are provided.The Dataset Used for training the model is taken kaggle.The dataset is filcker 8k. there different version of this dataset but i took 8k . the link to download the dataset are</br>

link1 : https://www.kaggle.com/datasets/jaykumar2862/flicker-8k </br>
link2 : https://www.kaggle.com/adityajn105/flickr8k</br>
link 1 is the dataset I used here for training.</br>
### STEPS:
- **Loading Dataset:**</br>
     - I downloaded the dataset directly from kaggle inthe nortebook  but you can download it local machine and load it in the notebook.
     
- **Extraxting Features from Images:**</br>
     - I used VGG 16 for Extracting Features from images which later passed to encoder and decoder model as input.
     - You can use any model to get image features.
     - The Size of the image is reduces to (224,224,).
     - The preprocesssing used is offical precoess used by VGG 16 model.
     - I have saved the features in dictionary form using pickle.
     
- **Loading and cleaning Captions:**</br>
    - Once we are done with Extractionof features then we load the captions from txt file
    - The we split those file into dictionary key as image name without extension and values as list of captions. Each image have different captions 
    - Then we clean the captions and add 'start' and 'end' as for indicating  as start of seq and end of sequence  
    
- **Vectorization of captions:**</br>
    - Once we clean the caption then we convert text captions into numbers using <code>Tokenizer</code> class from tensorflow.
    - Then we pafd the sequence to maxlenth using <code> pad_sequence </code> method
- **Train and test split:**</br>
    - Once we have done vectorix=zation its time to split into train and tes, Since we need to generate sequence we split each caption in below format.
    - Let us first see how the input and output of our model will look like. To make this task into a supervised learning task, we have to provide input and output to the model for training. We have to train our model on 6000 images and each image will contain 2048 length feature vector and caption is also represented as numbers. This amount of data for 6000 images is not possible to hold into memory so we will be using a generator method that will yield batches.

     - The generator will yield the input and output sequence.

          For example:

          The input to our model is [x1, x2] and the output will be y, where x1 is the 2048 feature vector of that image, x2 is the input text sequence and y is the                output text sequence that the model has to predict.


|x1(feature vector)	|x2(Text sequence)|y(word to predict)|
|------------------ |-----------------|------------------|
|feature	|start,	                          |two|
|feature	|start, two	|dogs|
|feature	|start, two, dogs	|drink|
|feature	|start, two, dogs, drink	|water|
|feature	|start, two, dogs, drink, water	|end|

**Models:**</br>
I have used VGG 16 model for getting features
