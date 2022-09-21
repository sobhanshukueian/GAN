# GAN 
GANs are generative models: they create new data instances that resemble your training data.
The **Generator** tries to produce data from some probability distribution. That would be you trying to reproduce the party’s tickets.
The **Discriminator** acts like a judge. It gets to decide if the input comes from the generator or the actual training set. That would be the party’s security comparing your fake ticket with the actual ticket to find flaws in your design.

![image](https://user-images.githubusercontent.com/47561760/191517152-f2c4d658-1631-4075-914e-75810b6532ed.png)

[Image Source](https://www.freecodecamp.org/news/an-intuitive-introduction-to-generative-adversarial-networks-gans-7a2264a81394)

The goal of the generator is to fool the discriminator, so the generative neural network is trained to maximize the final classification error (between actual and generated data)
The goal of the discriminator is to detect fake generated data, so 
the discriminative neural network is trained to minimise the final classification error.

## Loss
![image](https://user-images.githubusercontent.com/47561760/191520476-947a6fc0-3111-45da-a8c9-03643ae69faa.png)


# Dataset
The MNIST database of handwritten digits has a training set of 60,000 examples and a test set of 10,000 samples.
I used pytorch datasets for downloading dataset : 
```
train_dataset = datasets.MNIST('mnist/', train=True, download=True, transform=transform)
test_dataset = datasets.MNIST('mnist/', train=False, download=True, transform=transform)
```

#Model
In simple GAN, both discriminator and generator have simple architecture composed of fully connected layers, and we have leaky relu activation functions in the discriminator to prevent it from becoming zero and relu activation functions in the generator.

# Train
Trainer class Does the main part of code which is training model, plot the training process and save model each n epochs.

I Defined `Adam` Optimizer with learning rate 0.0002.

Each generative model training step occurse in `train_generator` function, descriminator model training step in `train_descriminator` and whole trining process in 
`train` function.

## Some Configurations
 
*   You can set epoch size : `EPOCHS` and batch size : `BATCH_SIZE`.
*   Set `device` that you want to train model on it : `device`(default runs on cuda if it's available)
*   You can set one of three `verboses` that prints info you want => 0 == nothing || 1 == model architecture || 2 == print optimizer || 3 == model parameters size.
*   Each time you train model weights and plot(if `save_plots` == True) will be saved in `save_dir`.
*   You can find a `configs` file in `save_dir` that contains some information about run. 
