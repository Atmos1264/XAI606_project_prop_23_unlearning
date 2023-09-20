# Applications and Practice in Neural Networks class project

## `Machine Unlearning`
### `Removing the influence of request subset of data without performance degradation`
### ([Neurips 2023 Machine Unlearning Challenge](https://www.kaggle.com/competitions/neurips-2023-machine-unlearning/overview))

<br/>
Deep Neural Networks enabled various applications and development in AI and has shown that it posseses much opportunity and potential. But at the same time, there exist inherent risks when it comes to privacy as large Neural Network models tend to memorize the details of their training set. It has been shown that even the training data can be reconstructed by the pre-trained model(<a href="https://giladude1.github.io/reconstruction/reconstruction_paper.pdf">Haim et al., [2022]</a>)

<br/>
This issue intrigues researchers to a new challenge which the objective is, when given a subset of data to be "forgotten", the model is processed to remove the influence of the subset data, when on the same time, not losing the performance with respect to the other remaining data.  

</br>

The dataset is unavailable for download, but consist of csv file which includes index of training(retain/forget)/validation set, images of people's faces, json file yieding a dict of age_class weights, and the original model.

**[retain/forget/validation].csv**

The training set is consist with retain set and forget set of image which is idexed with `image_id`
The images has individual indicators that can identify the particular data.

- `person_id` - A unique ID code for each subject
- `age_group` - Binned ages. The target label for the models.
- `age` - The age of the subject.
- `image_id` - A unique ID for the image. Includes the `person_id` to ensure each value is unique, line 'abc-1'.

**images/[person_id]/[image_id].png**

Images of people's faces. `images/foo/1.png` is indicated with image ID of `foo-1`. All the images are resized to 32x32 pixels. And contain approx. 30,000 images.(roughly 2% of the images in the dataset have idential perceptual hashes)

**age_class_weights.json**

The `age_group` weights to train the original model. Loading this file yields a dict of the form `{age_group: n_occurences}`.

**original_model.pth**

The original Resnet-18 Pytorch model checkpoint.
The model was trained to predict the age group with each image of a person's face. It was trained with class weights to mitigate class imbalance and no data augmentation. The original model obtains 99% accuracy on the training set and 96% on the test set with torch 1.13.1

</br>

To evaluate the unlearning algorithm by submitting your code in <a href="https://www.kaggle.com/competitions/neurips-2023-machine-unlearning/code">Kaggle</a>

You can also refer to the starting-kit released by Google
https://github.com/unlearning-challenge/starting-kit/tree/main