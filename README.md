# CSCI4931_DLFinal

This is where we will record all experiments and progress made in the pokemon type image classification.

Neural Networks: Convolutional Neural Networks

Progress Report
03/13: Image Data Collection
- for the image data collection, we are planning on using sample sprites from https://pokemondb.net/sprites/ to obtain the images needed for classification
- our other option is to use resized sprites from other previous works as our data samples like https://veekun.com/dex/downloads
- we plan on collecting our data samples and inputting them in folders by type, then  
- problem 1: some pokemon have appearance variants that change based on environmental factors (ex: Deerling, etc.)
  - toss out Pokemon #585, #586
- problem 2: some pokemon's type change based on environmental factors (ex: Castform, etc.)
  - include Pokemon that have variants that change type
  - Pokemon #493, #351

03/20: Image Processing and Creating Model
- Today, we focused on transferring the data samples to our repository and started framing our CNN model
- Some concerns we had were mainly on how to modify the model to output multiple labels for each pokemon and how to sort the images (?)
- We need to do more research on how to process the images and intially run the model
- We decided to obtain already made data samples that were sorted by generation and by type
- This is the video we are referencing to help us get started with processing the image data and building the CNN: https://www.youtube.com/watch?v=qFJeN9V1ZsI&t=4521s or https://deeplizard.com/learn/video/LhEMXbjGV_4
- Here is the site that has the most updated csv file of all the Pokemon's stats: https://www.kaggle.com/mariotormo/complete-pokemon-dataset-updated-090420?select=pokedex_%28Update.04.20%29.csv
  - The types for each Pokemon are the most updated from when they recently appeared, so our CNN will focus on deciding the most updated types for each Pokemon regardless of which generation and games they appeared in (since some Pokemon have had changed types based on the newer generations and games they have appeared in)
- Things to work on:
  - For processing the images, I noticed that a repository we are using the sprites for only have up to Gen V, so we need to add the sprites from Gen VI to Gen VII and sort them
  - For the sorting the leftover images, we will have to develop our own way to sort the images by type (cause there is no way we are doing it by hand) 
  - Also, I have not found a resource that has the pokemon sprites sorted for generations 6 - 8, so we might have to download them and sort it by generation/game :(
    - This is the closest site to having sprites for the other generations (have not looked at it myself yet): https://reliccastle.com/resources/383/  
  - Goal is to have a basic framework of our CNN that takes in one input and gives us one output and have all the data processed, organized by class, and shuffled

04/03: Editing Model to output primary Pokemon type
- Today, we added more convolutional and pooling layers to help analyze more features of our model. We also added 3 dropout layers with a dropout rate of 0.2 to reduce the overfitting problem in the model.
- During our model testing and experimentation, we altered the batch size, pooling filter size, and increased the number of epochs to 50.
- We also figured out why the outputs for some of the results of the test batch were all zero and fixed it so that it takes the maximum value out of all the values in the row versus checking each index of each row if they are > 0.5 to validate that they are apart of that class.
- Our goals now are to figure out how to see how close our test predicts are to the true test labels. (we have a function that checked how many of the predictions were correct)
  - 2nd goal is to make the neural network output 2 types instead of 1 (which will require some extra research).
  - Last goal (if there is time) is to work on obtaining and sorting images from generations 6 - 8 and add to the model.

04/10: Editing Model to output multiple types for each Pokemon
- Today, we did some research and decided to use a sigmoid activation function in the last layer for classifying multiple labels for each image. Using the sigmoid function will allow each image to be classified to each possible class independently of each other.
- For determining if the image fits in the class or not based on the given probability, we will find the two classes with the highest probabilities, where the first class is the primary type and the second class is the secondary type (still in progress). Another possibility is taking the output and for each class if the probability is greater than 0.5, then the image belongs to that class, but it will be hard to determine which is the primary and secondary types and risks getting an output where some images cannot be classified into a class (all 0s output). (Ask the professor about that) ****
- We also decided to move all the images classified in type 2 into the main folders so that Pokemons with multiple types can be classified. For example, Bulbasaur has two types (Grass and Poision), so Bulbasaur images will be placed in both Grass and Poison. For Pokemon that do not have a secondary type, another folder labeled 'None' will store those images of Pokemon with no second type.
- We also did some more testing and modified our architecture as needed to improve the accuracy and mean squared error of our model.
- We also decided to just stick with classifying 5 generations of Pokemon, since it would take extra time to obtain the images and save it to our local machines and code it to be sorted by primary and secondary types for Pokemons in generations 6-8 and all Pokemons in the games past generation 6.
- Other tasks done today:
  - Researched multi label CNN and implemented it into model
  - Researched other CNN architectures to help hyper tune parameters (kernel size, pool size, pooling function, number of convolutional layers, dropout rate, etc.)
  - Modified function to calculate accuracy of predicted test data set (problem encountered below)
- Some problems encountered or things to do in the future
  - Image Processing error?
  - Might need to research more on good metrics to help analyze model and results of data?
  - Need to edit architecture definitely, but that has been delayed due to implementing the multi label stuff.
  - Problem with interpretting output based on input.
    - We have 2 duplicate input images for each Pokemon and have placed them in two folders, one for the primary type and the second type. The model will be able to predict the labels, but there will be two outputs for the same image? We are having trouble trying to calculate the error of our test data given the ground truth (which is separated into two different outputs bc there are two duplicate images in different classes) and the predicted values (which will most likely be separated into two outputs bc there are duplicate images as input but for different classes). How do we calculate the error? Do we take the two outputs, calculate the error for the two classes, and average it somehow? ****
    - We plan on meeting with the Professor about our progress and confusion on 04/12

Questions about the Project
- How many data samples do we need for the project?
  - We were thinking of having sprites of each different pokemon from each generation, but are not sure if it would be enough data samples.
  - Will have to do more research on this for ourselves. We need at least 1 picture for every pokemon, but might need 5-6 images of each pokemon so the CNN can recognize the pokemons.
- Are we allowed to use python libraries to help design our neural networks or do we have to design them from scratch?
  - Use any python libraries available to help develop the CNN.
- Are we allowed to use data samples from other previous works? 
  - Yes, we can use data samples from other previous works.
- We want our neural networks to guess the two types for each Pokemon. Can the neural network have two outputs, and how will it work? 
  - Research Multilevel CNNs.
  - Here is a link for multi output CNNs by building two CNNs: https://towardsdatascience.com/building-a-multi-output-convolutional-neural-network-with-keras-ed24c7bc1178
  - Another link for multi output CNNs without having to build two CNNs: https://kaushal28.github.io/Building-Multi-Output-CNN-with-Keras/
  - Link #3 for multilabel CNN: https://towardsdatascience.com/multi-label-image-classification-with-neural-network-keras-ddc1ab1afede
- How should we handle special cases in our data samples? Should we include them or remove them? 
  - For now, leave in the special cases to see what the CNN will do.
