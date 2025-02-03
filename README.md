# CycleGAN for generating experimental data

The rise of machine learning (ML) for scientific research calls for large amounts of training data that sometimes may be infeasible to acquire. Generally, researchers want to label objects in images captured from microscopes or telescopes, so they may be tempted to train an ML model to do the labeling for them. Often, there is not enough training data for such models (one can only hand-label so many images). On the other hand, if there is some way of quickly generating lots of fake labeled images through a simulation, some processing can be done to make the simulated images look realistic so they can be used to train ML models. 

This repository builds a model that takes generated fake images, and makes them look real. This is done via image-to-image translation, and in particular, using a [cycleGAN](https://arxiv.org/abs/1703.10593) architecure. This repo has been used in research projects related to [STEM images of 2D materials](https://www.nature.com/articles/s41524-023-01042-3) and more recently to [images of bacterial colonies](https://arxiv.org/abs/2405.12407).

To get started, all you need are two folders. One containing a set of real images, and one containing a set of fake images. For minimal changes in the code, these images will need to be in TIF/TIFF format. You will also need the following modules installed (versions are the ones used for our work on bacterial segmentation):

* tensorflow (2.16.1)
* scipy (1.13.1)
* tensorflow_examples @ git+https://github.com/tensorflow/examples.git@0b14ce1c88537b94772cc99d995d936417be6f5d
* tifffile (2024.5.2)
* PIL (pillow 10.3.0)

We recommend using a device with an Nvidia GPU and CUDA installed (we used release 11.6, V11.6.55), as the code has not been tested on other hardware. In principle, any device able to use tensorflow should work.

There are 3 notebooks that you will run to get your desired set of generated images

1. `cycleGAN bin_cross.ipynb` - This notebook will train the cycleGAN. Once you have simulated and real images in their respective folder, assign their paths in the second cell. With a Nvidia 3090 GPU, this takes around 6-8 hours depending on the size of the dataset. 
  
2. `FID_Score.ipynb` - Once the training finishes, we need to choose the best training checkpoint that makes the generated images as close to the real images. This notebook will use the FID score between generated images from a given checkpoint and the real image dataset, and give the checkpoint with the lowest score.

3. `generator.ipynb` - Once we have the model trained and the best checkpoint, this notebook will take a folder of fake/simulated images and will make generated images from them.

If you have any questions, feel free to contact me:


Abid Khan: abid.a.khan@jpmchase.com
Vincent Hickl: vincent.hickl@empa.ch
