**Overview**

In this project, we aim to bypass the B4B (Bit-by-Bit) protection mechanism, 
which utilizes Locality-Sensitive Hashing (LSH) and noise addition based on hash bucket occupation.
Subsequently we want to query an encoder and steal it. 

We want to cluster the dataset in a way that our queries mimics a normal user and doesn't have a big coverage of embedded space. To achieve this, we implemented our notebook with following these steps:

* Project Feature Vectors: Reduce dimensionality of feature vectors using Principal Component Analysis (PCA).
  In this step our goal is to see how the data in the original dataset distributed. After the visualization we want to   cluster our data.

* Determine Optimal number of clusters: Use the Elbow Method and Silhouette Score to confirm the optimal number of clusters (see the visualization)

* Cluster the Projections: Apply K-Means clustering with number of clusters = 2 to the PCA projections. By using this method we have got K-Means Silhouette Score: 0.78534334897995, that indicates that we had optimal clusters. 

* Map Feature Vectors into LSH: Hash the feature vectors into LSH using the optimal number of hash buckets.

* Create Subsets: Generate subsets of the dataset based on clustering results.
  
* Retrieve original images for quering the target encoder for both clusters and visualize them to confirm they are saved correctly. 

* Save Subsets: Save the subsets as .pt files for further analysis.
  

* Obtain feature vectors by quering the target encoder and save it as .pt file
  
* Analyze the data for added noise. In this step we used different approaches like: PCA, t-sne and visualized the results of these algorithms to compare with the original representations and to detect the added noise. Also we tried to visualize the added noise by reversing the added cost function mentioned in the paper for B4B. It helped to indicate that the added noise was indeed gaussian noise and we could move forward. 
  
* First, we trained our encoder with obtained representation without denoising approach and got results with too big negative losses that was impossible to use for training

* Denoise the obtained feature vectors based on the results of the analysis (visualization and results are included in code). We used for this goal simple gaussian noise filtering.
  
* Use the denoised feature vectors to train an encoder that replicates the behaviour of the target encoder. After denoising the data, the training behaviour changed significantly that indicates that noise reduction helped. 
  
* Encoder is trained using SimSiam network and contrastive loss (cosine similarities used to calculate distances) to minimize the distance between represantations. 


All the files data used in the notebook are in the following [Google Drive](https://drive.google.com/drive/folders/1tBfVN5VosF7xBIGjrBZtR8KZuDyHOdPj?usp=drive_link)

