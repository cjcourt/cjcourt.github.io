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

[iMatGen]()
[Hoffmann et al.]()
[CrystalGAN]()
[Noh et al.]()

# How it works
## Representing Crystal Structures
A key problem with all machine learning problems is <b> How do we best represent our data?</b>. That is, how do we make the data machine-readable, so that the algorithm can learn meaningful features and therefore make predictions.

This is a difficult question for crystal structures, such as this one below:
![A typical Crystal](/images/dycro3.png)

Crystals have important properties and symmetries that need to be preserved when encoding into a machine-readable format. 

For our encoding we decided on a voxelised representation, whereby the crystal is represented by a 32x32x32 cube.

The value of each voxel is the local electron-density formed by the neighbouring atomic sites, e.g. each atom is represented by  Gaussian distribution, whose variance is directly proporional to the ion radius.

This essenially builds a 3-d electron-density map that looks something like this:

![Electron Density Map](/images/M.png)

Where the brighter regions have a higher electron-density than darker regions.

The question now is <b> How do we generate new electron-density maps?</b>
## VAE

## Unet

## CGCNN


## An Example - Generating Novel Perovkites

# Further Reading
The [paper](https://pubs.acs.org/doi/10.1021/acs.jcim.0c00464) and [source code](https://github.com/by256/icsg3d) for ICSG3D are  available for you to peruse at your leisure. 

