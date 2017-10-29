**Traffic Sign Recognition** 

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./Resources/TrainSample.png "Analysis of Training Sample"
[image3]: ./Resources/11_Rightofway.jpg "Right of Way"
[image4]: ./Resources/12_PriorityRoad.jpg "Priority Road"
[image5]: ./Resources/14_Stop.jpg "Stop Sign"
[image6]: ./Resources/17_Noentry.jpg "No Entry"
[image7]: ./Resources/25_RoadWork.jpg "Road Work"
[image8]: ./Resources/33_RightOnly.jpg "Right Only"


###Data Set Summary & Exploration

####1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the Collection library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 12630
* The size of test set is 4410
* The shape of a traffic sign image is 32x32x3
* The number of unique classes/labels in the data set is 43

####2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data ...

![alt text][image1]

###Design and Test a Model Architecture

####1. Data Processing.

Here, only original data set has been used, no data argumentation.
Color pictures are used as training input instead of grayscaled ones, because the former contains more useful info. 

All data should be normalized to 0 mean & 1 variance, considering numerical stability and efficiency of optimization.


####2. Model Architecture.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, same padding, outputs 28x28x10 	|
| RELU					|	Nonlinearization											|
| Max pooling	      	| 2x2 stride,  outputs 14x14x10 				|
| Convolution 5x5	    |  1x1 stride, same padding, outputs 10x10x20	|
| RELU					|	Nonlinearization											|
| Fully connected		| outputs 1*500        									|
| Fully connected		| outputs 1*200        									|
| Fully connected		| outputs 1*43        									|
| Softmax				| outputs Final Propability       									|
|						|												|

Comparing with LeNet, the max pooling for second layer has been deleted, because mas pooling will eliminated some useful info.
At the same time, the numbers of filter in each layer has been increased, pls refer to the above table.
Although the training result is satisfying, this may cause more overfitting problem.
 

####3. Model Training.

Epochs is set to 50, learning rate is 0.001, batch size is set to 128.
Larger epochs will give more confident results.

####4. Solution Approach

The LeNet architecture was chosen, because it's proved in previous proj for detecting info in grayscaled picture. Color picture has no big difference.  

As mentioned above, color picture has more info (maybe some of them are redundant), so no grayscaling has been done to the original data set. Then the max pooling of seccond layer has been deleted in order to keep more info. The filter numbers has been increased a little bit in order to get better result.

My final model results were:
* validation set accuracy is 0.939
* test set accuracy is 0.932
I trained the model several times with this final layout, the accuracy of validation set is in a range 0.935~0.96.

Several thing actually can be improved but haven't been tuned:
Dropout strategy with proper drop rate;
L2 regulation;
And progressive learning rate;
 
###Test a Model on New Images

####1. Acquiring New Images

Here are five German traffic signs that I found through google image:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]

The first image might be difficult to classify because ...

####2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Stop Sign      		| Stop sign   									| 
| U-turn     			| U-turn 										|
| Yield					| Yield											|
| 100 km/h	      		| Bumpy Road					 				|
| Slippery Road			| Slippery Road      							|


The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. This compares favorably to the accuracy on the test set of ...

####3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a stop sign (probability of 0.6), and the image does contain a stop sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .60         			| Stop sign   									| 
| .20     				| U-turn 										|
| .05					| Yield											|
| .04	      			| Bumpy Road					 				|
| .01				    | Slippery Road      							|

