# DNA_discriminator
Given a list of DNA sequences bound to an unknown Transcription Factor, we would like to gain insight into the binding preferences of this Transcription Factor and build a predictor that helps them identify novel sequences that would bind to it.
## File Structure and Reproduce Steps
    - **Train file - DNA_Discriminator.ipynb** : Train two discriminators respectively using reverse DNA sequence as negative data & using shuffled DNA sequence as negative data. Respectively, the trained models are saved to 'DNA_Discriminator.hdf5' (the one trained with reverse DNA sequence as negative data) and 'DNA_Discriminator_Shuffle.hdf5' (the one trained with shuffled DNA sequence as negative data).
 
    - **Test file - DNA_Test.ipynb** : Load the models from .hdf5 files, do the prediction on test dataset
    
    - **DNA_Discriminator.hdf5** : Trained model (reverse DNA sequence as negative data)
    
    - **DNA_Discriminator_Shuffle.hdf5** : Trained model (shuffled DNA sequence as negative data)
    
    - motif_plotter : A package to plot DNA motif
    

 
- To reproduce the model training via Google Colab, you need to upload the train.csv file to your Google drive path '/content/gdrive/My Drive', then run 'DNA_Discriminator.ipynb', 
- To reproduce the test part, you also need to upload the folder motif_plotter to your Google drive path '/content/gdrive/My Drive' (to plot the sequence motifs), and you also need to change the path of test data, namely, change ```path_test = F"/content/gdrive/My Drive/train.csv"``` to the path of your test data. 

If you would like to download and run the .py code, you need to edit the paths of storing train.csv and trained model.

## Architechture of DNN :
![alt text](https://github.com/GAOYUEtianc/DNA_discriminator/blob/main/Screen%20Shot%202021-09-30%20at%207.37.35%20AM.png)
- First there are two convolutional layers extracting features. 
- Then there are ReLu layers preventing 'dying ReLU' problem and speeding up training. 
- Then Max Pooing and Average Pooling are done in parallel to summarize the features. They summarize the features in different ways, so I used both of them.
- After flattening into Dim 1, it goes through a batch normalization to normalize the output of the previous layers, reducing the dependence of gradients on the scale of the parameters or their initial values. 
- Then it go through a fully connected layer, then dropout 50\% to reduce overfitting.
- Then it go through the last fully connected layer, and output a number in (0,1) using activation function - sigmoid, which corresponds to the probability of the sequence being a positive example.
## Train the model :
Since I don't have any test dataset, I used 80\% of the data (composed of positive labeled data and generated negative labeled data) as train dataset, and the remaining 20\% as test dataset.
## Evaluate the model :
After getting the model and predict it on test dataset, we can evaluate its performance by ROC and AUC since it's a binary classification. And the ROC\&AUC of the two models (respectively trained using reverse sequences and shuffled sequences as negative data) are plotted as follows :
Model 1  (Reversed DNA as negative data)                   |  Model 2 (Shuffled DNA as nagative data)
:---------------------------------:|:-----------------------------------:
![](https://github.com/GAOYUEtianc/DNA_discriminator/blob/main/Dis_1_ROC.png)  |  ![](https://github.com/GAOYUEtianc/DNA_discriminator/blob/main/Dis_2_ROC.png)

I also want to have a more intuitive insight to the binding preference of this TF, so I used motif_plotter to extract the learned motif.
