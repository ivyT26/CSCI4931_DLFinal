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
