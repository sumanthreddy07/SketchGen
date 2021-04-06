# SketchGen

Can a machine draw sketches like humans do? The paper [***A Neural Representation of Sketch Drawings***](https://arxiv.org/abs/1704.03477) presents a generative RNN which is capable of producing sketches of common objects, with the goal of training a machine to draw and generalize abstract concepts in a manner similar to humans. This repository presents examples of a simple sketchs (ex: ladder) to harder sketches (ex: cat).

<div align="center">
<img align="center" width="200" height="200" src="animations/animation_ladder0.gif"> 
<img align="center" width="200" height="200" src="animations/animation_cat0.gif">
</div>
<br>

> The implementation is ported from the official Tensorflow implementation that was released under project Magenta by the authors.

While there is a already a large body of existing work on generative modelling of images using neural networks, most of the work focuses on modelling raster images represented as a 2D grid of pixels. But this project presents a lower-dimensional vector-based representation inspired by how people draw.



## Overview
This project is based a Sequence to Sequence Variational Autoencoder (Seq2SeqVAE) in which we encode strokes (of a sketch) into a latent vector space, using a bidirectional LSTM as the encoder. The latent representation can then be decoded back into a series of strokes.

![](https://1.bp.blogspot.com/-iuML0km0cv0/WO6U0ukCaYI/AAAAAAAABt0/wsBg174LgtQslJgG2Q6jKeOTFP1EH3o3ACLcB/s1600/sketch_rnn.png)

The goal of a seq2seq autoencoder is to train a network to encode an input sequence into a vector of floating point numbers, called a latent vector, and from this latent vector reconstruct an output sequence using a decoder that replicates the input sequence as closely as possible. Since encoding is performed stochastically, and so is the sampling mechanism of the decoder, the reconstructed sketches are always different.

## Dependencies
- Tensorflow
- Python 3.8
- Ubuntu
- Google Colab

## Datasets
To train the model, the dataset required are available in the [Google Cloud Platform](https://console.cloud.google.com/storage/browser/quickdraw_dataset/sketchrnn). The dataset collected is from a game called quickdraw. The format of data is stroke 3 format which consists of x and y coordinates and a ‘0’ or ‘1’ denoting pen down and pen up.

## Training
The model can be trained directly from the [SketchGen.ipynb](SketchGen.ipynb) or can be locally run in the terminal using the below command

```bash
$ python3 seq2seqVAE_train.py <optional arguments>
```

### Important Optional Arguments (and their default values)
```bash
--data_dir          =   datasets
--experiment_dir    =   experiments
--epochs            =   20
```
> **NOTE: There are many more hyperparameters available in the file [seq2seqVAE.py](seq2seqVAE.py) which can be modified.**

### Using a pre-trained model
You can use the SketchGen.ipynb by providing the appropriate paths to all files and explore the sketchs in depth. There are examples of encoding and decoding of sketches, interpolating in latent space, sampling under different temperature values etc.

The Repo contains 4 pre trained models on Encoder_Size=256, Decoder_Size=512 latent_vector_space=128

- Cat (20 Epochs)
- Ladder (20 Epochs)
- Sun (20 Epochs)
- Leaf (20 Epochs)

## References
>1. David Ha and Douglas Eck, [***A Neural Representation of Sketch Drawings***](https://arxiv.org/abs/1704.03477), 2017
>2. David Ha, [***Teaching Machines to Draw***](https://ai.googleblog.com/2017/04/teaching-machines-to-draw.html), 2011
>3. [***Official Tensoflow Implementation***](https://github.com/magenta/magenta/tree/master/magenta/models/sketch_rnn) released under [***Project Magenta***](https://magenta.tensorflow.org/)