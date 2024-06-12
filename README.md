**Overview**

In this project, we aim to bypass the B4B (Bit-by-Bit) protection mechanism, 
which utilizes Locality-Sensitive Hashing (LSH) and noise addition based on hash bucket occupation.
Subsequently we want to query an encoder and steal it. 
To achieve this, we create subsets of a given dataset following these steps:

* Project Feature Vectors: Reduce dimensionality of feature vectors using Principal Component Analysis (PCA).

* Determine Optimal Clustering:Use the Elbow Method and Silhouette Score to confirm the optimal number of clusters.

* Cluster the Projections: Apply K-Means clustering to the PCA projections.

* Map Feature Vectors into LSH: Hash the feature vectors into LSH using the optimal number of hash buckets.

* Create Subsets: Generate subsets of the dataset based on clustering results.

* Save Subsets: Save the subsets as .pt files for further analysis.
  
* Visualize retrieved images: Visualized the clustered images to confirm they are saved correctly.
* Obtain feature vectors by quering the target encoder and save it as .pt file 
* Analyze the data for added noise
* Denoise the obtained feature vectors based on the results of the analysis (visualization and results are included in code)
* Use the denoised feature vectors to train an encoder 
