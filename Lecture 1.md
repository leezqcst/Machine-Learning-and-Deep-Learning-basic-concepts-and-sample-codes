# Basic concepts
- **Image classification** is a fundamental task for other Computer Vision problems (such as object detection, segmentation or image captioning).
- In computer view, an image is viewed as a **3-D array**. For a three color channels (RGB) image with 20 pixels wide, 30 pixels tall, it has a total of 20 * 30 * 3 = 1800 integers. Each integer ranges between 0 (black) and 255 (white). The image can be flatten out to be one dimensional array. For example, a specific 32x32 colour image of the [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) dataset can be flatten out to a 1x3072 numpy array of uint8s. The first 1024 entries contain the red channel values (row-major order, which means the first 32 entries are the red channel values of the *first row* of the image), the next 1024 the green, and the final 1024 the blue. see [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) for more detailed information.
- Machine learning approach is the **data-driven** approach. And all the available data can be split into training set, validation set and test set. Validation set (Cross validation) is used to select hyper-parameters, and test set is only used to report the accuracy **at a single time** in the end. Note that, when all the hyper-parameters are determined by cross validation, the final model is re-trained on (training set + validation set).
- Three approaches for image classification
  - k-nearest neighbor classifier, based on the pixel distance (L1 or L2). `k` and distance measure (L1 or L2) are determined by cross validation. The drawbacks of kNN are (1) storing all training set and (2) expensive predicting. Since totally different pictures may have the same distance, the performance of knn is not good. [FLANN](http://www.cs.ubc.ca/research/flann/) provides the implementaion. 
  - Linear classifier.
  - Convolutional Neural Network.

# Codes
## L1 and L2 distance between two vectors
```
a = np.array([1,2,3,4])
b = np.array([2,3,4,5])

# two strategies for L1
np.linalg.norm(a-b, ord=1) # 4
np.sum(np.abs(a-b)) # 4

# two strategies for L2
np.linalg.norm(a-b) # 2.0
np.sqrt(np.sum(np.square(a-b))) # 2.0
```
## Euclidean distance between two matrix
```
train = np.random.random((5,3))
test = np.random.random((8,3))

# stratege 1
train_square = np.sum(np.square(train), axis=1) # shape: (5L,)
test_square = np.sum(np.square(test), axis=1, keepdims=True) # shape(8L, 1L)
train_test = np.dot(test, train.T) # (8L, 5L)
res = np.sqrt(-2*train_test + train_square + test_square) # (8L, 5L)

# strategy 2
from scipy.spatial.distance import cdist
res_scipy = cdist(test, train, metric='euclidean')
```
# Part solution of Assignment 1 

Reference: http://cs231n.github.io/classification/