# Assignment 4

## Table of Contents
- [Task 1: CLIP Dissect](#task-1-clip-dissect)
  - [Data and Methodology](#data-and-methodology)
  - [Visualization](#visualization)
  - [Findings and Conclusion](#findings-and-conclusion)
- [Task 2: LIME](#task-2-lime)
  - [Methodology](#methodology)
  - [Results](#results)
  - [Observations](#observations)
  - [Conclusion](#conclusion)
- [Task 3: Grad-CAM](#task-3-grad-cam)
  - [Methodology](#methodology-1)
  - [Results](#results-1)
  - [Conclusion](#conclusion-1)
- [Task 4: Comparison of LIME and Grad-CAM](#task-4-comparison-of-lime-and-grad-cam)
  - [Data Preparation](#data-preparation)
  - [IoU Calculation](#iou-calculation)
  - [Results](#results-2)
  - [Analysis](#analysis)
  - [Insights](#insights)
  - [Conclusion](#conclusion-2)
- [References](#references)

## Task 1: CLIP Dissect

In this task, we analyzed the internal representation of neurons in the last 3 layers (i.e., fc, layer4, layer3) of the ResNet18 model trained on two separate datasets: ImageNet and Places365. We used Network Dissect via the CLIP Dissect library to label neurons with the concepts they have learned.

### Data and Methodology

By using the `describe_neurons.py` script from the CLIP-dissect repository, we labeled each neuron in the specified layers of the models. The script assigns the most relevant label to each neuron based on its activation patterns. We used these labels to plot multiple graphs for a better understanding of the concepts learned by each layer.

### Visualization

We created two types of visualizations to understand the learned concepts:
- Bar graphs showing the top 20 frequent neuron concept labels learned by each layer in both models.
- Scatter plots depicting the similarity scores of neuron activations across the top 20 concepts for each model.

Figures 1 & 2 correspond to the plots for ResNet(ImageNet), and Figures 3 & 4 correspond to ResNet(Places365).

### Findings and Conclusion

- **ImageNet Model:** The fc layer showed a high frequency of neurons associated with specific object categories. Lower layers (layer3, layer4) contained neurons responding to more abstract features. The similarity plots indicated that the model learns specific object categories at the fc layer.
- **Places365 Model:** The fc layer learned scene categories, while lower layers contained abstract and structural concepts. Similarity plots showed higher similarity values for abstract and structural concepts in lower layers and increased similarity scores for scene categories at the fc layer.

From these observations, we conclude that the two models have different representations of concepts due to the characteristics of the datasets.

## Task 2: LIME

LIME (Local Interpretable Model-agnostic Explanations) generates interpretations by explaining the model in subgroups around nearest neighbor points. It acts as a simple model locally approximating to the black box, showing which features of input were important for generating the prediction.

### Methodology

We used the LIME code and applied the technique to ten ImageNet images to generate explanations by using a simple model like linear locally approximating to the model. This shows which features are important in the prediction.

### Results

We generated images with the top 10 positive features from LIME methods. Yellow boundaries define the significant features for the prediction.

### Observations

- **Gold Fish:** Highlighted body and fins, showing these features were key for the prediction.
- **Tiger Shark:** Highlighted parts of the body and fins.
- **Kite:** Highlighted wings and tail.
- **Vulture:** Highlighted head and neck.
- **Iguana:** Highlighted head, scales, and texture.
- **Flamingo:** Emphasized legs and neck.
- **American Coot:** Highlighted head and body.
- **West Highland White Terrier and Human:** Highlighted faces and eyes.
- **Racing Car:** Highlighted front and sides, logo, and aerodynamic features.
- **Orange:** Focused on the texture and color of the fruit.

### Conclusion

LIME helps us understand and trust the model’s predictions better by highlighting the important features of each image.

## Task 3: Grad-CAM

Grad-CAM visualizes the regions of input images that contribute most to the predictions of a neural network model. We also compared Grad-CAM with other methods like LIME and extended the analysis using AblationCAM and ScoreCAM.

### Methodology

- **Grad-CAM:** Computes the gradient of the target class score with respect to the feature maps of the last convolutional layer.
- **AblationCAM:** Systematically ablates parts of the network and observes the change in output.
- **ScoreCAM:** Generates a heatmap without using gradients, perturbing the input image and measuring the change in target score.

### Results

- **Grad-CAM:** Highlighted the head and fins of the fish.
- **AblationCAM:** Highlighted regions near the head and upper body.
- **ScoreCAM:** Presented a smoother heatmap, focusing on the head and fin.

### Conclusion

CAM methods effectively highlight critical regions influencing the model’s predictions. Grad-CAM provides better insights than LIME by marking a more compact and useful area.

## Task 4: Comparison of LIME and Grad-CAM

We compared LIME and Grad-CAM results with the same set of images, evaluating IoU (Intersection over Union) of the highlighted regions.

### Data Preparation

- Processed the images and created explanatory masks.
- LIME 1 uses top 10 features with only positive impact.
- LIME 2 includes both positive and negative impacts.

### IoU Calculation

Computed as the ratio of the intersection to the union of the two masks.

### Results

| Image | IoU1 (LIME 1 vs Grad-CAM) | IoU2 (LIME 2 vs Grad-CAM) |
|-------|----------------------------|---------------------------|
| Kite | 0.3177 | 0.3177 |
| Orange | 0.3878 | 0.3457 |
| Vulture | 0.3900 | 0.3570 |
| West Highland white terrier | 0.4457 | 0.3845 |
| Tiger shark | 0.3664 | 0.3664 |
| American coot | 0.4087 | 0.3853 |
| Flamingo | 0.2799 | 0.5343 |
| Common Iguana | 0.2894 | 0.2894 |
| Goldfish | 0.2828 | 0.2828 |
| Racer | 0.2306 | 0.2282 |

### Analysis

- **Simpler Images:** Lower IoU indicates LIME and Grad-CAM place importance on different areas even in simple scenarios.
- **Complex Images:** Low IoU shows disagreement on key regions.
- **LIME 1 vs LIME 2:** Including both positive and negative features in LIME does not consistently lead to better alignment with Grad-CAM.

### Insights

- **Method Agreement:** Generally low, reflecting different mechanisms of identifying important regions.
- **Feature Selection:** Varies with image complexity and nature.
- **Image Complexity:** Variability in IoU indicates complexity alone does not determine method agreement.

### Conclusion

There are considerable differences in the highlighted regions by Grad-CAM and LIME. These findings emphasize the necessity of using multiple explanation techniques to understand model behavior comprehensively.

## References

1. [CLIP Dissect](https://github.com/Trustworthy-ML-Lab/CLIP-dissect)  
   A repository for dissecting the CLIP model and understanding its features and components.

2. [Task-1 Implementation](https://github.com/balwanishivam/tml-assignment/blob/Assignment-4/Assignment-4/task-1/interpretation.ipynb)  
   Implementation details and code for Task-1 of the assignment, which includes model interpretation techniques.

3. [LIME](https://github.com/marcotcr/lime/blob/master/doc/notebooks/Tutorial%20-%20images%20-%20Pytorch.ipynb)  
   A tutorial notebook for using LIME (Local Interpretable Model-agnostic Explanations) with image data in PyTorch.

4. [Task-2 Implementation](https://github.com/balwanishivam/tml-assignment/tree/Assignment-4/Assignment-4/task-2)  
   Implementation details and code for Task-2 of the assignment, focusing on different model interpretability methods.

5. [Grad CAM](https://github.com/jacobgil/pytorch-grad-cam?tab=readme-ov-file#using-from-code-as-a-library)  
   A library for implementing Grad-CAM (Gradient-weighted Class Activation Mapping) for visualizing model predictions.

6. [Task-3 Implementation](https://github.com/balwanishivam/tml-assignment/tree/Assignment-4/Assignment-4/task-3)  
   Implementation details and code for Task-3 of the assignment, which includes visualization techniques using Grad-CAM.

7. [Task-4 Implementation](https://github.com/balwanishivam/tml-assignment/blob/Assignment-4/Assignment-4/task-4/iou.ipynb)  
   Implementation details and code for Task-4 of the assignment, focusing on Intersection over Union (IoU) metrics.

8. [Clip Dissect Library](https://github.com/Trustworthy-ML-Lab/CLIP-dissect/blob/main/describe_neurons.py)  
   A script for describing and analyzing neurons in the CLIP model, useful for understanding model behavior.

9. [Plots for Task-1](https://github.com/balwanishivam/tml-assignment/tree/Assignment-4/Assignment-4/task-1/results)  
   Visualizations and plots generated from Task-1 implementation results.

10. [Result Images for Task-2 (LIME)](https://github.com/balwanishivam/tml-assignment/tree/Assignment-4/Assignment-4/task-2/results/boundary_1/images)  
    Result images showcasing the LIME interpretability method applied in Task-2.

11. [Result Images for Task-3 (GradCAM)](https://github.com/balwanishivam/tml-assignment/tree/Assignment-4/Assignment-4/task-3/results)  
    Result images showcasing the Grad-CAM visualization technique applied in Task-3.

Note: To generate this README from Report PDF we used ChatGPT.