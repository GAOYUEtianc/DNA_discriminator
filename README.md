# DNA_discriminator
Given a list of DNA sequences bound to an unknown Transcription Factor, we would like to gain insight into the binding preferences of this Transcription Factor and build a predictor that helps them identify novel sequences that would bind to it.
## Architechture of DNN :
![alt text](https://github.com/GAOYUEtianc/DNA_discriminator/blob/main/Screen%20Shot%202021-09-30%20at%207.37.35%20AM.png)
First there are two convolutional layers extracting features, then there are ReLu layers preventing 'dying ReLU' problem and speeding up training. Then Max Pooing and Average Pooling are done in parallel to summarize the features. After flattening into Dim 1, it goes through a batch normalization to normalize the output of the previous layers, reducing the dependence of gradients on the scale of the parameters or their initial values. Then it go through a fully connected layer, then dropout 50\% to reduce overfitting, then it go through the last fully connected layer, and output a number in (0,1) using activation function sigmoid.
## File Structure
### - Train file
### - Test file
