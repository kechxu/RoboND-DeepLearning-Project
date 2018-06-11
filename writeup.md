[image_0]: ./figures/my_plot.png
[image_1]: ./figures/hero.png
[image_2]: ./figures/non_target.png
[image_3]: ./figures/patrol_with_targ.png
[image_4]: ./figures/training_curves.png
[image_5]: ./figures/final_score.png

## Neural Network Architecture
- Input layer (3 features)
- Encoding layers (32, 64, 64) - increase depth for more information
- 1x1 convolution layer - retain spatial information
- Decoding layer (64, 64, 32) - upsample layers to retain spatial information, also contains skip connections

## Neural Network Diagram
![alt text][image_0]
## Neural Network Parameters
- `learning_rate = 0.003` The learning rate was made small so the network would converge to a lower minimum. However, because of the lower learning rate, the number of epochs needed to be increased so the cost of the neural network could properly be minimized
- `batch_size = 30` The batch size was lowered for faster training.
- `num_epochs = 15` Due to the limitations of time, it was decided to keep the number of epochs as low as possible. It was incrementally changed from 5 to 15 epochs through testing. Since the learning rate was lowered, more epochs were needed to minimize the cost.
- `validation_steps = 50` Kept as default
- `workers = 2` Kept as default

## Neural Network Techniques
### 1x1 convolutions
A 1x1 convolution is used to preserve spatial information as well as make neural networks deeper to model more complex relationships. They are relatively inexpensive since they are just another matrix multiplication.

### Fully connected layers
Fully connected layers should be used when spatial information does not matter such as classifying a single object, or predicting an abstract value. However, due to the nature of the problem, 1x1 convolutions are preferred because of they retain spatial information.

### Skip connections
Skip connections allow for cleaner segmentations as it gives access to information from different levels of the filter. By incorporating information from different convolution layers in the network, the spatial information can be more accurate.

### Encoding
Encoding reduces the height and width of the convolution in favour of more features/depth. This can extract higher levels of information or features that may not be immediately present in shallower levels. To retain the spatial information lost from encoding, decoding and skip connections are used.

### Decoding
Due to the encoding process, the segmented portions of the image can be recognized but there is a loss of spatial information. The process of decoding allows the network to regain the spatial information, specifically locating where the segmented object is located within the dimensions of the original image. This is done from Bilinear upsampling. Skip connections are also used to gain more accurate spatial information.

## Results
The following is a summary of the results. The full html file can be viewed at `code/model_training.html`
### Training curve
![alt text][image_4]
### following_images
![alt text][image_1]
### patrol_non_targ
![alt text][image_2]
### patrol_with_targ
![alt text][image_3]
### Final score
![alt text][image_5]
The final score is 0.43 accuracy. Since the accuracy is greater than 40%, the project is a success.

## Applications of the Neural Network
Although the trained model is able to locate humans within given images, its application to other class segmentation is limited. Other objects like dogs, cats, or cars would not be properly segmented since the training set did not contain those kinds of objects as well as the training. If it was necessary to expand the network's functionality, new training data would be needed and the neural network may need to modified to adjust to the new images.

## Future Enhancements
The results were disappointing since it is not very accurate. It was difficult to understand the effects of hyperparameter tuning as they caused different results. In the scope of the project, I tried to limit the amount of parameters I tuned to 2 or 3 so I could focus on them. Ideally, it would be better to tune all of the parameters to fully optimize the network.

The greatest limitation for this project was the time constraints. Training networks with more layers were more time expensive and if they required hyperparameter tuning, would need a lot of time to optimize. If more time was available, I would try different network architectures to see which one has the most potential.

Another idea to explore is to implement dropout in the network. As shown in the training graph, there was a large increase in cost at the 6th epoch. It's not clear what happened but it is possible that the training data was much different in comparison to the first 5 epochs. Dropout could potentially create more redundancies in the network so that the network is more robust in terms of handling unknown images.

The final enhancement I would consider implementing is a script that would tabulate the performance of each neural network I trained. This way, I could see the comparative performances of different neural networks based on their hyperparameter tuning. This would help a lot when going through the neural network architecture changes.

With these enhancements, it is likely to improve the accuracy of the neural network significantly.
