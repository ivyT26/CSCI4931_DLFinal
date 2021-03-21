# CSCI4931_DLFinal

This is where we will record all experiments and progress made in the pokemon type image classification.

Neural Networks: Convolutional Neural Networks

Progress Report
03/13: Image Data Collection
- for the image data collection, we are planning on using sample sprites from https://pokemondb.net/sprites/ and https://veekun.com/dex/downloads to obtain the images needed for classification
- our other option is to use resized sprites from other previous works as our data samples
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
- This is the video we are referencing to help us get started with processing the image data and building the CNN: https://www.youtube.com/watch?v=qFJeN9V1ZsI&t=4521s or https://deeplizard.com/learn/video/LhEMXbjGV_4
- Here is the site that has the most updated csv file of all the Pokemon's stats: https://www.kaggle.com/mariotormo/complete-pokemon-dataset-updated-090420?select=pokedex_%28Update.04.20%29.csv
  - The types for each Pokemon are the most updated from when they recently appeared, so our CNN will focus on deciding the most updated types for each Pokemon regardless of which generation and games they appeared in (since some Pokemon have had changed types based on the newer generations and games they have appeared in)
- Things to work on:
  - For processing the images, I noticed that a repository we are using the sprites for only have up to Gen V, so we need to add the sprites from Gen VI to Gen VII and sort them
  - For the sorting the leftover images, we will have to develop our own way to sort the images (cause there is no way we are doing it by hand) 
  - Goal is to have a basic framework of our CNN that takes in one input and gives us one output and have all the data processed, organized by class, and shuffled

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
  - Another linkt for multi output CNNs without having to build two CNNs: https://kaushal28.github.io/Building-Multi-Output-CNN-with-Keras/
- How should we handle special cases in our data samples? Should we include them or remove them? 
  - For now, leave in the special cases to see what the CNN will do.
