# Semantic Segmentation
### Introduction
The objective of this project is to label the pixels of roads in images using a Fully Convolutional Network (FCN) architecture based on the paper "Fully Convolutional Networks for Semantic Segmentation" by Long, Shelhamer, and Darrell. 

### Code Dependencies
##### GPU
`main.py` will check to make sure you are using GPU - if you don't have a GPU on your system, you can use AWS or another cloud computing platform.
##### Frameworks and Packages
Make sure you have the following is installed:
 - [Python 3](https://www.python.org/)
 - [TensorFlow](https://www.tensorflow.org/)
 - [NumPy](http://www.numpy.org/)
 - [SciPy](https://www.scipy.org/)
 - [Python Image Library (PIL)](https://pillow.readthedocs.io/) for SciPy's `imresize` function.

##### Dataset
Download the [Kitti Road dataset](http://www.cvlibs.net/datasets/kitti/eval_road.php) from [here](http://www.cvlibs.net/download.php?file=data_road.zip).  Extract the dataset in the `data` folder.  This will create the folder `data_road` with all the training a test images.

##### Run
Run the following command to run the project:
```
python main.py
```
**Note:** If running this in Jupyter Notebook system messages, such as those regarding test status, may appear in the terminal rather than the notebook.

#### Example Outputs
Here are examples of a sufficient vs. insufficient output from a trained network:

Sufficient Result          |  Insufficient Result
:-------------------------:|:-------------------------:
![Sufficient](./examples/sufficient_result.png)  |  ![Insufficient](./examples/insufficient_result.png)

### Code Architecture
The code in 'main.py' downloads a pre-trained VGG16 model and extracts the input and keep probability layers as well as layers 3, 4, and 7. The remainder of the network architecture was constructed using these layers.

- conv_1x1_l7: 1x1 convolutional layer (input - VGG16 layer 7)
- output_l7: 4x4 deconvolution layer with stride of 2 (input - conv_1x1_l7)
- conv_1x1_l4: 1x1 convolution layer (input - VGG16 layer 4)
- output_l7: Addition of output_l7 and conv_1x1_l4 (skip layer)
- output_l4: 4x4 deconvolution layer with stride of 2 (input - output_l7)
- conv_1x1_l3: 1x1 convolution layer (input - VGG16 layer 3)
- output_l4: Addition of output_l4 and conv_1x1_l3 (skip layer)
- output_l3: 16x16 deconvolution layer with stride of 8 (input - output_l4)


### Results
The results from the classification of pixels in test road images is given in the 'runs' folder. The following is a sample of the results.

![Road](Run.gif)
