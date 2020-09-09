---
title: "ICSG3D"
excerpt: "3D Inorganic Crystal Structure Generation<br/><br/><img src='/images/toc.png' width=200px>"
collection: projects
---

# Overview
Deep generative models are very cool. They utilise deep neural networks to approximate a data distribution in a way that can be sampled to produce novel samples. This has been applied to music, text, speech, faces and more. For intance, these faces below were generated using [StyleGan](https://github.com/NVlabs/stylegan). Creepy right?

![These people don't exist](/images/stylegan.png)

This poses the question: <i>Can we use generative models to make new materials?</i>

If we could, then we could generate thousands of new materials (chemicals, drugs, molecules, crystals etc.) for potential device applications - think deep-fakes for materials. This would revolutionise materials discovery, which is traditionally an arduous process.

To explore this, [Batuhan Yildirim](https://by256.github.io) and I developed ICSG3D, a complete pipeline for generating 3-D crystal structures and simultaneously predicting their properties.

# Related Work
There are a few other studies that have attempted to use generative models for crystal structure generation. The predominant ones are:

[iMatGen](https://www.sciencedirect.com/science/article/pii/S2590238519301754)
[Hoffmann et al.](https://arxiv.org/abs/1909.00949)
[CrystalGAN](https://arxiv.org/abs/1810.11203)
[Kim et al.](https://arxiv.org/abs/2004.01396)

# How it works
## Representing Crystal Structures
A key problem with all machine learning problems is <b> How do we best represent our data?</b>. That is, how do we make the data machine-readable, so that the algorithm can learn meaningful features and therefore make predictions.

This is a difficult question for crystal structures, such as this one below:
![A typical Crystal](/images/dycro3.png)

Crystals have important properties and symmetries that need to be preserved when encoding into a machine-readable format. 

For our encoding we decided on a voxelised representation, whereby the crystal is represented by a 32x32x32 cube.

The value of each voxel is the local electron-density formed by the neighbouring atomic sites, e.g. each atom is represented by  Gaussian distribution, whose variance is directly proporional to the ion radius.

This essentially builds a 3-d electron-density map that looks something like this:

![Electron Density Map](/images/M.png)

Where the brighter regions have a higher electron-density than darker regions.

The question now is <b> How do we generate new electron-density maps?</b>

## VAE
![VAE](/images/crystal_vae-1.png)
The first step of the ICSG3D pipeline "learns" a representation of these electron-density maps (which I shall denote $M$) using a Variational Autoencoder (VAE). 

Technically speaking, a vanilla VAE is a probabilistic latent variable model that estimates the intractable posterior distribution of the input samples using a deep-neural network. 

In simple terms, a VAE attempts to "compress" the inputs in such a way that the compressed representation <i>encodes</i> meaningful characteristics. 

 The architecture consists of an encoder network, $E$, and decoder network, $D$ that are jointly trained to encode and reconstruct the inputs. In our case, the model is trained to reconstruct input electron-density maps, $M$, such that the latent vector, $\mathbf{z}$, at the bottleneck, encodes semantically meaningful characteristics of the crystal structures.

 So in simple terms, we put in an electron-density map, $M$, the VAE creates a representation of this sample, and spits out a reconstructed version $M'$, that we hope is as close to the input as possible.

 Then, to create new samples, all we have to do is sample from the bottleneck, and decode the vector to create new samples.

 There are other important aspects to the VAE used in our paper, such as propery-conditioning,  coordinate convolutions and deep-feature consistency. See the paper for more details.

## Unet
![Unet](/images/unet.png)
The next stage of the process takes the generated electron-density map ($M'$) and attempts to determine the original atomic coordinates using a Unet semantic segmentation network. 

This network labels each voxel with the atomic number of the corresponding site. Creating 3-d "blobs" as seen in the image above.

From these blobs we can find the centroids and determine the atomic coordinates.

## CGCNN
![CGCNN](/images/gnn-1.png)
Finally, we use a Crystal Graph Convolution Neural Network (CGCNN) to predict the properties of the created crystals. This representation treats crystals as directed graphs, in which nodes (atoms) are connected by edges (bonds). This naturally lends itself to representing crystals. The seminal work by Tian Xie is [here](https://arxiv.org/abs/1710.10324) if you're interested.

## Results
![Results](/images/rand_gens-1.png)
The results are completely novel crystals! that have been shown to be valid and stable by electronic-structure calculations.

# Further Reading
The [paper](https://pubs.acs.org/doi/10.1021/acs.jcim.0c00464) and [source code](https://github.com/by256/icsg3d) for ICSG3D are  available for you to peruse at your leisure. 

I intend to do a blog on creating and validating new materials at some point, so keep an eye out.

