
# What Are You Eating?

This is my COGS 109 Final Project where we attempted to create a model that can predict what fruit (apple, banana, orange, or pineapple) an image is of.

## Methods
This model works by taking in each pixel in the image as an input, and the existence of each fruit (represented as 0 or 1) as the output, using ~4500 images as training data. First the model uses [PCA (Principal Component Analysis)](https://en.wikipedia.org/wiki/Principal_component_analysis) to reduce the number of input parameters greatly, from 100x100x3 (length x width x rgb) input parameters to only 20. Then it uses [K-fold cross validation](https://en.wikipedia.org/wiki/Cross-validation_(statistics)#k-fold_cross-validation) to choose an optimal number of principal components to use. Finally we use logistic regression to actually train the model. 

After doing PCA, we can reconstruct the images using our 20 PCs. With our first dataset (COCO dataset), the images were too complex so 20 PCs were not sufficient to reproduce the original image. 

![Coco original 1](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/prePCA1.png)![Coco PCA 1](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/postPCA1.png)

Left: Original image  ---------------------- Right: After PCA Reconstruction

![Coco original 2](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/prePCA2.png)![Coco PCA 1](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/postPCA2.png)

Left: Original image  ---------------------- Right: After PCA Reconstruction

Due to the inaccurate reconstructions of the original images, we decided to use the Kaggle dataset, [Fruits 360](https://www.kaggle.com/moltean/fruits). These images are a lot less complicated, so the reconstructions are a lot better.

![Kaggle PCA 1](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/applePCA1.png)![Kaggle PCA 2](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/applePCA2.png)![Kaggle PCA 3](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/bananaPCA.png)

Above: After PCA Reconstruction
Below: Original Image

## Results
The model will make a prediction between 0 to 1 for each category of fruit the image could be. Generally, predictions for bananas work the best (probably because of its unique shape and color). Below I will show some example predictions for its own training data, as well as real life images outside of the training data. 

###  Predictions on Training Data
![trainingApple](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/trainingApple.png)![trainingBanana](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/trainingBanana.png)![trainingOrange](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/trainingOrange.png)![trainingPineapple](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/trainingPineapple.png)
###  Predictions on Real Life Photos
![testOrange](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/testBanana.png)![testOranges](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/testOrange.png)![testBanana](https://raw.githubusercontent.com/FrankWan27/WhatAreYouEating/master/report%20images/testOranges.png)


## Getting Started

### Prerequisites
- Jupyter Notebook 
- Python 3+
- Standard Python Libraries (Numpy, Pandas, Sci-Kit Image, Sci-Kit Learn)

### Installing COCO API 
Only do this if you want to use the COCO dataset

#### Linux  

- To install pycocotools from https://anaconda.org/conda-forge/pycocotools
- Open terminal
```
	conda config --add channels conda-forge

	conda install pycocotools
```
	
#### Windows 	

- We will use https://github.com/philferriere/cocoapi, because pycocotools is not supported by Windows
- Run anaconda shell
```	
	conda install git
	
	pip install git+https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI
```
### How To Run
- Open "What Are You Eating Kaggle PCA.ipynb" in Jupyter Notebook
- Run the code blocks from top to bottom to run predictions on the training data
- If you would like to use your own images, change the test image name in the last two code blocks to the image of your choice, then run the second to last code block immediately before running PCA, and the last code block after running PCA. 
