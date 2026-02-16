Image Denoising and Reconstruction Using Autoencoders
**1. Project Overview**

This project implements an image denoising autoencoder using TensorFlow and Keras. The model is trained to reconstruct clean images from corrupted inputs. Multiple types of synthetic distortions are applied to the training data to simulate real-world image degradation.

The goal of the project is to explore how autoencoders learn image reconstruction and to analyze reconstruction artifacts such as smoothing and loss of fine details.

2. Objectives

Implement a custom image corruption pipeline

Train an autoencoder to reconstruct clean images from distorted versions

Evaluate reconstruction quality

Analyze the effect of the loss function on output sharpness

Understand why blurring occurs in autoencoder outputs

**3. Methodology**
3.1 Autoencoder Architecture

The model consists of:

Encoder

Input layer matching image dimensions

Convolutional layers

Compression into a latent representation

Decoder

UpSample layers

Reshaping to original image shape

Sigmoid output activation to produce pixel values in the range [0, 1]

The model is trained using:

Optimizer: Adam

Loss function: Mean Squared Error (MSE)

**4. Image Corruption Pipeline**

Training images are artificially degraded before being fed to the network. The applied corruptions include:

4.1 Gaussian Noise

Additive noise sampled from a normal distribution.

4.2 Blur

Gaussian blur applied to simulate loss of detail.

4.3 Brightness Distortion

Global brightness scaling using a random factor.

4.4 Color Channel Perturbation

Each RGB channel is scaled independently using random factors within a controlled range.

All pixel values are clipped to the valid range [0, 1] after corruption.

**5. Experimental Observations**
5.1 Reconstruction Performance

The trained autoencoder is capable of:

Reducing noise

Correcting color distortions

Normalizing brightness levels

5.2 Blurring in Reconstructed Images

The reconstructed images appear slightly smoother than the original ground truth images.

This behavior is expected and occurs due to:

The use of Mean Squared Error (MSE), which encourages pixel-wise averaging.

The averaging behavior of autoencoders when uncertain about high-frequency details.

The use of fully connected layers, which do not explicitly preserve spatial structure.

As a result, high-frequency features such as edges and fine textures are partially smoothed.

6. Limitations

Fully connected architecture does not optimally preserve spatial relationships.

MSE loss tends to produce smoother outputs.

Fine textures and sharp edges may not be fully reconstructed.

**7. Possible Improvements**

Future enhancements may include:

Introducing skip connections (U-Net style architecture)

Using perceptual or SSIM-based loss functions

**8. Requirements**

Python 3.x

TensorFlow / Keras

NumPy

Matplotlib

OpenCV (optional)

Install dependencies using:

pip install tensorflow numpy matplotlib opencv-python
