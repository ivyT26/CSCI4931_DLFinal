# CSCI4931_DLFinal

This is where we will record all experiments and progress made in the pokemon type image classification.

Neural Networks: Convolutional Neural Networks

Progress Report
03/13: Image Data Collection
- for the image data collection, we are planning on using sample sprites from https://pokemondb.net/sprites/bulbasaur to obtain the images needed for classification
- our other option is to use resized sprites from other previous works as our data samples
- we plan on collecting our data samples and inputting them in folders by type, then 
- problem 1: some pokemon have appearance variants that change based on environmental factors (ex: Deerling, etc.)
  - toss out Pokemon #585, #586
- problem 2: some pokemon's type change based on environmental factors (ex: Castform, etc.)
  - include Pokemon that have variants that change type
  - Pokemon #493, #351

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
  - Here is a link for multi output CNNs: https://towardsdatascience.com/building-a-multi-output-convolutional-neural-network-with-keras-ed24c7bc1178
- How should we handle special cases in our data samples? Should we include them or remove them? 
  - For now, leave in the special cases to see what the CNN will do.
