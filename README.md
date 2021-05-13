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
 
 04/18: Ivy's offline work
 - Researched ways to oversample dataset for more even distribution. Implemented option 1 in the code. 
   - 1) random oversampling: choosing random images from current dataset in each class to duplicate
   - 2) weights: using higher weights for minority classes that have less data than majority classes
   - 3) using SMOTE: a library to oversample dataset (usually used for string data)
 - Undersampling is not advised because having more data gives more information about the patterns the model can learn, and undersampling loses data information in exchange for eqaul distribution of data for each class.
 - I have emailed the professor, but have not gotten a response back about using a single model compared to multiple classification models to implement multilabel classification, so on my end I have decided to work with both models. The first one is where there are two models that classify type 1 and type 2 using softmax in last layer and categorical cross entropy loss function, and the second model is a single model that classifies the top 2 most probable classes using sigmoid in last layer and a binary cross entropy loss function.
   - For the 2 classification models, the datasets will be separated into type 1 and type 2, and within each folder the Pokemon's primary type will be sorted into 1 of 18 types in the type 1 folder, while the Pokemon's secondary type will be sorted into 1 of 19 types (includes None, where a Pokemon may not have a second type) in the type 2 folder. 
   - For the single classification model, the datasets will be stored into one folder with subfolders holding each type, where duplicates of a single Pokemon will be located in 2 folders, the first picture in its primary type and the second picture in its secondary type. (ie. a Bulbasaur image will be stored in the 'Grass' class and the 'Poison' class)
- By the end of 04/19, I should have the oversampling code done for both models (today I just have the code implemented for the first model that has two classification models). If there is time for me on 04/19, I will research other models and see how the current models can be improved upon.
- Links for multilabel classification
  - https://www.geeksforgeeks.org/an-introduction-to-multilabel-classification/
  - https://kgptalkie.com/multi-label-image-classification-on-movies-poster-using-cnn/
  - https://gsurma.medium.com/image-tagger-multi-label-cnn-image-classification-5b0a87f0084d
  - https://machinelearningmastery.com/multi-label-classification-with-deep-learning/
  - https://towardsdatascience.com/journey-to-the-center-of-multi-label-classification-384c40229bff
- Links for oversampling and coding it
  - https://machinelearningmastery.com/random-oversampling-and-undersampling-for-imbalanced-classification/
  - more links in the comments of the given code
- Future works: I really would love to work on this project and improve on it for generations 6-8, which will take a lot of data collection on my part. Also, I would like to explore more efficient classification models and more accurate metrics to measure efficiency of classification models in the near future. 

04/26: Ivy's offline work Pt 2
- I emailed the professor regarding issues about training the model.
- After making many modifications such as changing the types of layers, number of layers, kernel size, number of filters, acivation functions, adding dropout and batch normalization layers, etc., but the model never improved.
- Professor responded and advised me to preprocess the data using mena subtraction, or normalization, given the link: https://cs231n.github.io/neural-networks-2/#datapre

5/02: Updating model and testing it with oversampled data
- We resolved the problem with Ivy's laptop not being able to run the model, so we have to rely on Brady's PC to run everything.
- We planned out test cases to run the models for type 1 and 2, implemented oversampling to create equal class distribution, and included data augmentation for overfitting problem.
- We also worked on the project presentation. (outline finished)
- Plan on meeting again on 05/07 to finish the project report. 
- Github should be updated with test results/observations and updated code of the models soon.

5/07-5/13: Brady's offline work
- Ran a list of tests we created over several days and recorded obseravtions
  - Observations
  - With a dropout of .2 the model seems to be overfitting very quickly. However, we obtained a very good accuracy for predicting type 2
  - Added data augmentation because the model still seemed to be overfitting.
  - The data augmentation is making the model learn very slowly so I am taking out the dropout layers to see if it learns quicker and gets a higher accuracy.
  - Even with taking out dropout layers the model was significantly worse. It decreased the accuracy by nearly 20%. Therefore, we decided not to use the data augmentation and   revert to our previous data.
    -After running through all our test cases I chose the top two tests and ran them again but instead of 50 epochs I ran with 600 epochs. The model produced 67.18% accuracy for type 1 and 88.55% accuracy for type 2. Combine the model had a 59.49% accuracy.
- After all the tests were done created confusion matrices to display our data
- Finished up the section on results in our final lab report

Questions about the Project
- How many data samples do we need for the project?
  - We were thinking of having sprites of each different pokemon from each generation, but are not sure if it would be enough data samples.
  - Will have to do more research on this for ourselves. We need at least 1 picture for every pokemon, but might need 5-6 images of each pokemon so the CNN can recognize the pokemons.
- Are we allowed to use python libraries to help design our neural networks or do we have to design them from scratch?
  - Use any python libraries available to help develop the CNN.
- Are we allowed to use data samples from other previous works? 
  - Yes, we can use data samples from other previous works.
- We want our neural networks to guess the two types for each Pokemon. Can the neural network have two outputs, and how will it work? 
  - Research Multilabel CNNs.
  - Here is a link for multi output CNNs by building two CNNs: https://towardsdatascience.com/building-a-multi-output-convolutional-neural-network-with-keras-ed24c7bc1178
  - Another link for multi output CNNs without having to build two CNNs: https://kaushal28.github.io/Building-Multi-Output-CNN-with-Keras/
  - Link #3 for multilabel CNN: https://towardsdatascience.com/multi-label-image-classification-with-neural-network-keras-ddc1ab1afede
- How should we handle special cases in our data samples? Should we include them or remove them? 
  - For now, leave in the special cases to see what the CNN will do.
