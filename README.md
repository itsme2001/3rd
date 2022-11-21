link--https://colab.research.google.com/drive/13mIHuJM4L9sPEWfvJWQmWnwANEhD_4YJ?usp=sharing

############################################################


import tensorflow as tf
from tensorflow import keras 
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import random

# Load the training and testing data MNIST
# Import dataset & split into train and test data
fminst=tf.keras.datasets.fashion_mnist
(x_train,y_train),(x_test,y_test)=fminst.load_data()

len(x_train)
len(y_train)

len(x_test)
len(y_test)

# Shape of the training dataset
x_train.shape

# Shape of the testing dataset
x_test.shape

# See first Image Matrix
x_train[0]

# See first image
plt.matshow(x_train[0])

# Normalize the iamges by scaling pixel intensities to the range 0,1
x_train=x_train/255
x_test=x_test/255
# See first Naormalize Image Matrix
x_train[0]

# Define the network architecture using Keras
model=keras.Sequential([
    keras.layers.Flatten(input_shape=(28,28)),
    keras.layers.Dense(128,activation ='relu'),
    keras.layers.Dense(20,activation='softmax')
])
model.summary()

from IPython.core import history
# Compile the Model

model.compile(loss='sparse_categorical_crossentropy', optimizer='sgd' ,metrics=['accuracy'])
history=model.fit(x_train,y_train,validation_data=(x_test,y_test),epochs=10)

#Evaluate the network
test_loss,test_acc=model.evaluate(x_test,y_test)
print("Loss=%.3f" %test_loss)
print("Accuracy =%.3f"%test_acc)

# Making Prediction on New Data
n=random.randint(0,9999)
plt.imshow(x_test[n])
plt.show()

predicted_value=model.predict(x_test)
print("Image is =%d" %np.argmax(predicted_value[0]))

class_labels=["T - shirt / top","Trouser","Pullover","Dress","Coat","Sandal","Shirt","Sneaker","Bag","Ankle boot"]
class_labels[np.argmax(predicted_value[0])]

# Plot the training loss and accuracy
history.history.keys()
dict_keys=(['loss', 'accuracy', 'val_loss', 'val_accuracy'])
plt.plot(history.history['accuracy'])
plt.plot(history.history['val_accuracy'])
plt.plot(history.history['loss'])
plt.plot(history.history['val_loss'])
plt.title('Training Loss & Accuracy')
plt.ylabel('accuracy/loss')
plt.xlabel('epoch')
plt.legend(['loss', 'accuracy', 'val_loss', 'val_accuracy'])
plt.show()
