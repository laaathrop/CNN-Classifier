# Robot Perception Enabled by a Multiclass Image Classifier

#### Introduction 

The goal of this project was to develop an image classifier that will function as the driving force behind decision making for an autonomous robotic vehicle that will eventually have the ability to classify and seek out different objects within a room space. This kind of technology may be useful for consumers that wish to take advantage of the increasing accessibility of household robotics; this kind of image classification technology could also be used in a manufacturing setting for differentiating between objects, humans, animals and equipment and could be used as the basis for a safety mechanism that protects humans from being injured by robots while they manufacture goods.

The original intent of this project was to use an image classifier in conjunction with a small camera mounted on top of an autonomous Field Programmable Gate Array (FPGA) based robotic vehicle in order to empower the vehicle to differentiate between different types of objects and make decisions based on the whereabouts of the objects. Some of the project functionality has been slated for future project goals.

#### Exploratory Data Analysis

The CIFAR-100 image dataset was chosen as the basis for this image classifier mainly for its inclusion of small objects and foods that would commonly be found in any given room within a household, corporate setting, education setting, etc. The inclusion of other various flora and fauna could serve to benefit applications of an image classifier to machine safety mechanisms. The CIFAR 100 dataset contains 100 classes containing 600 images within each class. Additionally, the 100 classes are grouped into 20 superclasses. Each image has two class labels, one coarse (a more general object category) and one fine (a more specific object category). Each image has a width of 32 pixels, a length of 32 pixels and 3 color channels: Red, Green and Blue.

The input data used to train the model could be tailored for more specific applications by adding or removing classes but for the purposes of this project, all of the original images were used.

#### Preprocessing

The image pixel data was scaled by 255 so that each pixel shade value would fall between 0 and 1. The original NumPy array containing the training was then reshaped for model generation and ended up being a 4-Dimensional tensor of size (60000, 32, 32, 3).

#### Modeling

The image classifier was built using a convolutional neural network (CNN) that also made use of MaxPooling, Flattening and Dropout Regularization. Sparse Categorical Crossentropy was used as the loss function for the CNN model because of its ability to predict integer targets without having to one-hot encode the target variables. Finally, the model was fit and validated. The final scores after 10 epochs were as follows:

Fine Class Accuracy - 0.51
Fine Validation Accuracy - 0.39

Coarse Class Accuracy - 0.55
Coarse Validation Accuracy - 0.49

The drop in accuracy scores between training and testing indicates an overfit model, for which there are several solutions. Given more time I'd like to take steps to increase the accuracy scores via the following methods:

1) Implement a GridSearching algorithm to optimize the model. This was attempted prior to the current model but failed due to matrix size errors.

2) Implement a Residual Net layer. This was also attempted prior to the current model and failed due to matrix size incompatibility issues.

3) Implement a solution that would localize objects within images for more accurate detection.

4) Augment the data

#### Visualizations

Four visualizations were created for the CNN model, two to show the training and testing loss by epoch and two to show the training and testing accuracy by epoch. In general, the loss decreased and the accuracy increased as the number of epochs increased. The the case of the fine class predictions, the testing loss actually did fluctuate, there was not a consistent trend and the loss did increase for some epochs.

#### Executive Summary

Relevant stakeholders mentioned in the introduction include consumers of household machines and robots, manufacturers of household machines, manufacturers of manufacturing machines and consumers of manufacturing machines. For each of these relevant stakeholders I would recommend using an image classifier for the following reasons:

1) The ability to differentiate between animals, humans, equipment and other types of objects could enhance a machine's ability to shut off or execute other safety related functions. 

2) To go a step further, a machine has the potential to use an image classifier to differentiate between itself and another machine. Autonomous machines might be able to use this feature to coordinate between each other, forming teams and lending a helping hand whenever possible.

#### References and Citations

I would like to acknowledge Jannik Zurn, a German PhD student that wrote the following article: 

https://medium.com/@jannik.zuern/training-a-cifar-10-classifier-in-the-cloud-using-tensorflow-and-google-colab-f3a5fbdfe24d

I adapted a considerable amount of his code to fit the needs of my project and his use of data augmentation and residual network layers inspired some of the future goals of my project.

#### Future Project Goals

The device mentioned in the introdution consists of a Field Programmable Gate Array that is mounted on a chassis with light sensing technology and currently has the ability to autonomously follow narrow areas atop a surface that lack color by controlling the duty cycle of two electric motors attached to the vehicle, causing it to follow black paths on a surface.

Goal 1 - Write a Python module that will allow an iPhone to capture images and preprocess them for use with FPGA developer tools.

Goal 2 - Write a module in the Verilog hardware description language that would allow for the vehicle to make decisions about it's actions based on the classified images input from the real time image feed.

