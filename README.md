# Tensorflow Image Classifer-for-poets

My first tensorflow training to train an image classifier. Thanks to [Google codelab developers](https://github.com/googlecodelabs)

To run [TensorFlow](https://www.tensorflow.org/) on a single machine, and will train a simple classifier to classify images of flowers.

The exact codelab tutorial can be found [here](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/#0). It is very helpful.

Using transfer learning, we have to start using a model that has been already trained, which will help us retrain final later of already trained model with new categoies from start. This time we will be using MobileNet instead of inception V3 aritechture. This is because Inception V3 is optimized for accuracy and performance, while the MobileNets are optimized to be smaller in size and efficient but lower acccuracy performance compared to inception v3.

However, I will be retraining it on a similiar task. 
Reason is because it takes lesser time, and deep learning takes many days to train a model. 

Personally I am using docker quickstart terminal: info [here](https://docs.docker.com/toolbox/toolbox_install_windows/)
on how to install docker for windows if you are using windows like me.

![](./gif1.gif)

## Objectives:
+ to use python and tensorflow to train an image classifer 
+ to classify images with my trained classifer 




## 1. Install tensorflow in terminal (you can use your normal command prompt or docker terminal) 

```
-> pip install --upgrade tensorflow, 
(require python 3.5, or python 3.6.4 but im using python 3.5.2)
```

## 2. Training of dataset can be done with the following steps:
Clone the git respository by typing 

```
git clone https://github.com/googlecodelabs/tensorflow-for-poets-2
```


## 3. Download the dataset 
Use this link to download the [flower data](http://download.tensorflow.org/example_images/flower_photos.tgz). Then extract the flower photos from the .tgz file just downloaded nad paste it in the tf_files folder. The folder contains 5 categories, daisy, roses, dandelion, sunflower, tulips and a License.txt.file.



## 4. MobileNet Config
Open command promt or docker terminal and type:

```
IMAGE_SIZE=224
ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"
```


## 5. Start TensorBoard

```
tensorboard --logdir tf_files/training_summaries &
```


## 6. train the model
Open command promt or docker terminal and type:

```
cd tensorflow-for-poets-2
python -m scripts.retrain \
  --bottleneck_dir=tf_files/bottlenecks \
  --how_many_training_steps=500 \
  --model_dir=tf_files/models/ \
  --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
  --output_graph=tf_files/retrained_graph.pb \
  --output_labels=tf_files/retrained_labels.txt \
  --architecture="${ARCHITECTURE}" \
  --image_dir=tf_files/flower_photos
```

## 7. Retrain Model and improve accuracy  
remove the parameter --how_many_training_steps to use 4000 iterations 
```
python -m scripts.retrain \
  --bottleneck_dir=tf_files/bottlenecks \
  --model_dir=tf_files/models/"${ARCHITECTURE}" \
  --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
  --output_graph=tf_files/retrained_graph.pb \
  --output_labels=tf_files/retrained_labels.txt \
  --architecture="${ARCHITECTURE}" \
  --image_dir=tf_files/flower_photos
  ```
  
![](./Capture1.PNG)
