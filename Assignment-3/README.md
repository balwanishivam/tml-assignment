# Assignment-3

## Description
We have tried to train a model robust. In order to do that we have implimented the following algorithm.

* Clean Training: We trained a clean resnet 50 model. We trained the model with early stopping and saved the weights. Then we retrained the trained model with reshuffled data and we observe a better accuracy.

* PGD Training: After training the model on clean data we used the same trained weights and started training using PGD without random start and again retrain the model with shuffled data and we observe a better accuray after training using data shuffling. 

* Additional Approaches: 
  * We also tried training the model with PGD attack and random start with l2 norm then retrain the model with l(inf) norm.
  * We also tried training the model with PGD attack with random start.

## Shadow Models
Access the trained models via the following Google Drive link: [Trained Out Models](https://drive.google.com/drive/folders/1N6BdTbHrzdXmjFRM5zmEHCqhAPFULBSX?usp=sharing)


