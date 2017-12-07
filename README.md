# Capsule Network - notMNIST and affNIST Dataset
A Tensorflow implementation of CapsNet on notMNIST and affNIST dataset based on Geoffrey Hinton's paper [Dynamic Routing Between Capsules](https://arxiv.org/abs/1710.09829)

## Datasets ##
1) [notMNIST](http://yaroslavvb.blogspot.com/2011/09/notmnist-dataset.html) which contatins letters from 'A' to 'J' and can be used for validating if a given algorithm is generic and can work outside the MNIST dataset.

2) The [affMNIST](http://www.cs.toronto.edu/~tijmen/affNIST/) dataset for machine learning is based on the well-known MNIST dataset. MNIST, however, has become quite a small set, given the power of today's computers, with their multiple CPU's and sometimes GPU's. affNIST is made by taking images from MNIST and applying various reasonable affine transformations to them. In the process, the images become 40x40 pixels large, with significant translations involved, so much of the challenge for the models is to learn that a digit means the same thing in the upper right corner as it does in the lower left corner. 

Research into "capsules" has suggested that it is beneficial to directly model the position (or more general "pose") in which an object is found. affNIST aims to facilitate that by providing the exact transformation that has been applied to make each data case, as well as the original 28x28 image. This allows one to train a model to normalize the input, or to at least recognize in which ways it has been deformed from a more normal image. 

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg?style=plastic)](https://opensource.org/licenses/Apache-2.0)


> 1.Capsule - A new version neural unit(vector in vector out, not scalar in scalar out)
> 2.Routing algorithm - similar to attention mechanism

## Requirements
- Python
- NumPy
- [Tensorflow](https://github.com/tensorflow/tensorflow) (I'm using 1.3.0, not yet tested for older version)
- tqdm (for displaying training progress info)
- scipy (for saving images)

## Usage
**Step 1.** Download this repository with ``git`` or click the [download ZIP](https://github.com/naturomics/CapsNet-Tensorflow/archive/master.zip) button.

```
$ git clone https://github.com/naturomics/CapsNet-Tensorflow.git
$ cd CapsNet-Tensorflow
```

**Step 2.** Download the [notMNIST](https://github.com/davidflanagan/notMNIST-to-MNIST.git)

- a) Unzip the same into the data/notMNIST

```
$ mkdir -p data/notMnist
$ gunzip data/notMnist/*.gz
```

**Step 3.** Start the training(Using the notMNIST dataset by default):

```
$ python main.py
$ # or training for fashion-mnist dataset
$ python main.py --dataset fashion-mnist
```

**Step 4.** Calculate test accuracy

```
$ python main.py --is_training=False
$ # for fashion-mnist dataset
$ python main.py --dataset fashion-mnist --is_training=False
```

> **Note:** The default parameters of batch size is 128, and epoch 50. You may need to modify the ``config.py`` file or use command line parameters to suit your case, e.g. set batch size to 64 and do once test summary every 200 steps: ``python main.py  --test_sum_freq=200 --batch_size=48``

## Results

- training loss

![total_loss](results/total_loss.png)
![margin_loss](results/margin_loss.png)
![reconstruction_loss](results/reconstruction_loss.png)

- test accuracy(using reconstruction)

Routing iteration | 1 | 2 | 3 |
:-----|:----:|:----:|:------|
Test accuracy | 0.43 | 0.44 | 0.49 |
*Paper* | 0.29 | - | 0.25 |

![test_acc](results/routing_trials.png)


![capsVSneuron](imgs/capsuleVSneuron.png)

### Reference
- [naturomics/CapsNet-Tensorflow](https://github.com/naturomics/CapsNet-Tensorflow): Capsule Network Implementation
- [XifengGuo/CapsNet-Keras](https://github.com/XifengGuo/CapsNet-Keras): referred for some code optimizations
