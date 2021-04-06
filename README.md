# SketchGen

Can a machine draw sketches like humans do? In the paper [***A Neural Representation of Sketch Drawings***](https://arxiv.org/abs/1704.03477), it presents a generative RNN which is capable of producing sketches of common objects, with the goal of training a machine to draw and generalize abstract concepts in a manner similar to humans. This repository presents examples of a simple sketchs (ex: ladder) to harder sketches (ex: cat).

While there is a already a large body of existing work on generative modelling of images using neural networks, most of the work focuses on modelling raster images represented as a 2D grid of pixels. In this paper, it presents a lower-dimensional vector-based representation inspired by how people draw.

The implementation is ported from the official Tensorflow implementation that was released under project Magenta by the authors.

<div align="center">
<img align="center" style="float: center;" width="200" height="200" src="animations/animation_ladder0.gif"> 
<img align="center" style="float: center;" width="200" height="200" src="animations/animation_cat0.gif">
</div>

## Overview
This project is a Sequence to Sequence Variational Autoencoder (Seq2SeqVAE) in which we encode strokes (of a sketch) into a latent vector space, using a bidirectional LSTM as the encoder. The latent representation can then be decoded back into a series of strokes.

The goal of a seq2seq autoencoder is to train a network to encode an input sequence into a vector of floating point numbers, called a latent vector, and from this latent vector reconstruct an output sequence using a decoder that replicates the input sequence as closely as possible. Since encoding is performed stochastically, and so is the sampling mechanism of the decoder, the reconstructed sketches are always different.

## Dependencies
- Tensorflow
- Python 3.8
- Ubuntu
- Google Colab

## Usage
### Training

To train the model, the dataset required are available in the [Google Cloud Platform](https://console.cloud.google.com/storage/browser/quickdraw_dataset/sketchrnn) 

```bash
python3 seq2seqVAE_train.py
```

#### Important Optional Arguments (and their default file names)
```bash
--data_dir          =   datasets
--experiment_dir    =   experiments
--epochs            =   20
```
**NOTE: There are many more hyperparameters available in the [seq2seqVAE.py](seq2seqVAE.py) which can be modified.**

### Using a pre-trained model
You can use the SketchGen.ipynb by providing the appropriate paths to all files and explore the sketchs in depth. There are examples of encoding and decoding of sketches, interpolating in latent space, sampling under different temperature values etc.

The Repo contains 4 pre trained models
- Cat (20 Epochs)
- Ladder (20 Epochs)
- Sun (20 Epochs)
- Leaf (20 Epochs)

## References
>1. David Ha and Douglas Eck, [***A Neural Representation of Sketch Drawings***](https://arxiv.org/abs/1704.03477), 2017
>2. David Ha, [***Teaching Machines to Draw***](https://ai.googleblog.com/2017/04/teaching-machines-to-draw.html), 2011
>3. [Official Tensoflow Implementation](https://github.com/magenta/magenta/tree/master/magenta/models/sketch_rnn), [Project Magenta](https://magenta.tensorflow.org/)