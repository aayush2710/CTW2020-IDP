# Wireless Outdoor Localization
## IEEE CTW 2020 Data Competition

Aim - Estimate position of a user in an outdoor environment using channel state information obtained on antenna array.

[Problem Statement](http://ctw2020.ieee-ctw.org/wp-content/uploads/sites/94/2020/02/CTW2020-Localization-Competition.pdf)


### Dataset Details
Channel responses were measured between a moving transmitter and an 8*8 antenna array. Out of 64 only 56 antenna were functional.

Labelled Dataset
1. Channel response (56x924X2X5)
2. Position (1X3)
3. SNR (1X16)

Unlabelled Dataset
1. Channel response (56x924X2X5)
2. SNR (1X16)

A total of 4979 labelled and 36192 unlabelled samples were provided.

Download link

hdf5 format - https://www.dropbox.com/sh/nvgox5e6udpkqni/AACpTPwdQI_8jkRZjHlOGfqPa?dl=0

Compared to CTW2019, this competition provided a large amount of unlabelled data to to evaluate the potential of self-supervised learning for user localization based on CSI.


### Algorithms Tested

#### Supervised CNN 
For this algorithm, we did not utilize the unlabelled data and trained a Deep Convolutional Network to estimate position. Implementation is available [here](SupervisedCNN.ipynb).

#### PCA and CNN (Semi Supervised)
We trained PCA to smoothen the output of each antenna on the unlabelled dataset. Deep CNN was trained on labelled dataset to estimate position. Implementation is available [here](PCA&CNN.ipynb).

#### AutoEncoder and CNN (Semi Supervised)
We used a convolutional autoencoder to reduce dimension of input CSI. The Auto encoder was trained on unlabelled dataset. This model was used to extract features on labelled dataset which were used to train a position estimator. The Implementation is available [here](AE&CNN.ipynb).

#### Siamese Neural Networks (Semi Supervised)
We trained a deep convolutional network on both labelled and unlabelled sets. We used sammon mapping algorithm to train on unlabelled dataset. Pairs were selected from unlabelled set and the network was backpropogated to keep distance between CSI and position proportional by a trainable parameter α. The same network was also trained via supervised means on labelled set. Implementation is available [here](SiameseNN.ipynb)

#### TRRS (Self Supervised)
We tried labelling unlabelled data using TRRS and train a network on both labelled and unlabelled(Now self labelled) sets. However performance of TRRS in labelling wasn't accurate enough on this dataset. Implementation is available [here](TRRS_2020.ipynb)


#### Performance

| Algorithm         | Mean RMSE(m)  |
| ------------------|:-------------:|
| Supervised CNN    | 13m           |
| PCA + CNN         | 65.12m        |
| AE + CNN          | 42.46m        |
| Siamese NN        | 59.21m        |

### Team
1. [Aayush Goyal](https://github.com/aayush2710)
2. [Kuntal Kokate](https://github.com/Kkuntal990)
3. [Krati Arela](https://github.com/krati012)

### Supervisor

Dr. Sai Dhiraj Amuru

Adjunct Assistant Professor, IIT Hyderabad

Hyderabad, India

E-mail: [asaidhiraj@iith.ac.in](mailto:asaidhiraj@iith.ac.in)

### References

1. Christoph Studer, Saeıd Medjkouh, Emre Gon ultas Tom Goldstein, and Olav Tirkkonen- Channel Charting: Locating Users within the Radio Environment using Channel State Information

2. Eric Lei, Oscar Castañeda ,Olav Tirkkonen ,Tom Goldstein and Christoph Studer- Siamese Neural Networks for Wireless Positioning and Channel Charting
