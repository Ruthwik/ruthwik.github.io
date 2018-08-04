---
layout: post
title: Neural Networks 101  - Part 1
subtitle: Build your first Neural network.
published: true
categories: machinelearning
gh-repo: Ruthwik/StockPrediction
tags: [deep learning, TensorFlow, python, neural networks]
bigimg:
  - /img/tensorflownutshell/tensorflowimage.jpg

---

<div class="text-justify">
<p>TensorFlow is a multipurpose Opensource software library for numerical computation using data flow graphs. It is originally developed by Google Brain Team to conduct deep neural networks research. TensorFlow is written in Python, C++ and CUDA. It provides stable Python API,C APIs and without backwards compatability gaurantee  C++, Go, Java, JavaScript and Swift. TensorFlow is applied in a wide variety of domains as well.The following figure shows how SketchRNN built using TensorFlow will complete your sketch in multiple ways.
</p>

<img src="/img/tensorflownutshell/magenta.gif" alt="magenta"/>
<p> <&emsp> Source: magenta.tensorflow.org </p>


<p> In this tutorial I	will cover the very	basics of TensorFlow. Deep learning will be covered in a different post. I will be using TensorFlow's Python API to explain.	

<h3>Installing TensorFlow</h3> 
<p>TensorFlow is a library and it can be installed like any other library using <code>pip</code> command.
<ul>
  <li>Install python 3.6 and above. Download from <a href="https://www.python.org/downloads//">here.</a></li>
  <li>Install Tensorflow <pre><code>pip3 install --upgrade tensorflow</code></pre></li>
</ul>
</p>
> Note: We will be using TensorFlow with CPU support only. If you have supporting GPU then please see these <a href="https://www.tensorflow.org/install/">instructions.</a>


<h3>Tensors</h3> 
<p>Let's us first understand what are tensors and the reference that we can take to get going.</p>
<p>A scalar is a physical quantity that it represented by a dimensional number
at a particular point in space and time. Examples are hydrostatic pressure
and temperature.</p>
<p>A vector is a bookkeeping tool to keep track of two pieces of information
(typically magnitude and direction) for a physical quantity. Examples are
position, force and velocity.
</p>
<p>
<code>What happens when we need to keep track of three pieces of information
for a given physical quantity?</code>
</p>

>  Tensors are geometric objects that describe linear relations between geometric vectors, scalars, and other tensors. Elementary examples of such relations include the dot product, the cross product, and linear maps. Geometric vectors, often used in physics and engineering applications, and scalars themselves are also tensors.

<img src="/img/tensorflownutshell/tensors.png" alt="magenta"/>

<p>
A Tensor has the following properties:
</p> 
<img src="/img/tensorflownutshell/tensor_rank.jpg" alt="magenta"/>

<p>
The rank of a tensor is its number of dimensions.The shape of a tensor is the number of elements in each dimension
</p>
| Rank          | Shape              | Dimension number  | Example                                 |
| ------------- |:------------------:| :----------------:| --------------------------------------: |
| 0             | []                 | 	0-D  			 | A 0-D tensor. A scalar.                 |
| 1             | [D0]               | 	1-D 			 | A 1-D tensor with shape [5].            |
| 2             | [D0, D1]           | 	2-D 			 | A 2-D tensor with shape [3, 4].         |
| 3             | [D0, D1, D2]       | 	3-D 			 | A 3-D tensor with shape [1, 4, 3].      |
| n             | [D0, D1, ... Dn-1] | 	n-D  			 | A tensor with shape [D0, D1, ... Dn-1]. |

<p>
The following image shows the various quantity.
</p>
<img src="/img/tensorflownutshell/tensor_scalar_vector.jpg" alt="magenta"/>
<p>
In simple terms Tensors are called as multidimenional arrays.
</p>

<h3>Computational graphs</h3> 
<p>
TensorFlow internally represent the operations and performs its computation using a data flow graph (or computational graph). In other words
Tensorflow approaches series of computations as a flow of data through a graph with nodes being computation units and edges being flow of Tensors.
</p>	
<img src="/img/tensorflownutshell/tf.gif" alt="magenta"/>

<h3>Importing TensorFlow</h3> 
<p>We will now divide the dataset into two parts for training and testing. Scikit provides <code>train_test_split(*arrays, **options)</code> to split the dataset.
By default, test_size value is set to 0.25 and train_size value is set to 0.75. We can change these values according to our needs.
<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>

<h3>Constants</h3> 
<p>We will now divide the dataset into two parts for training and testing. Scikit provides <code>train_test_split(*arrays, **options)</code> to split the dataset.
By default, test_size value is set to 0.25 and train_size value is set to 0.75. We can change these values according to our needs.
<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>

<h3>Variables</h3> 
<p>We will now divide the dataset into two parts for training and testing. Scikit provides <code>train_test_split(*arrays, **options)</code> to split the dataset.
By default, test_size value is set to 0.25 and train_size value is set to 0.75. We can change these values according to our needs.
<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>

<h3>Session</h3> 
<p>We will now divide the dataset into two parts for training and testing. Scikit provides <code>train_test_split(*arrays, **options)</code> to split the dataset.
By default, test_size value is set to 0.25 and train_size value is set to 0.75. We can change these values according to our needs.
<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>

<h3>Placeholders</h3> 
<p>We will now divide the dataset into two parts for training and testing. Scikit provides <code>train_test_split(*arrays, **options)</code> to split the dataset.
By default, test_size value is set to 0.25 and train_size value is set to 0.75. We can change these values according to our needs.
<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>

<h3>TensorBoard</h3> 
<p>We will now divide the dataset into two parts for training and testing. Scikit provides <code>train_test_split(*arrays, **options)</code> to split the dataset.
By default, test_size value is set to 0.25 and train_size value is set to 0.75. We can change these values according to our needs.
<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>

<p>
Before concluding let's predict the price of the apple stock on a given day. 
<script src="https://gist.github.com/Ruthwik/331de409f77d68147353978fbbc08844.js"></script>
</p>
<p>I hope you liked this tutorial. You can find the complete code on my github <a href="https://github.com/Ruthwik/StockPrediction">StockPrediction</a>. 
If you want to learn more about maths behind Linear Regression or ML in general, do check the following resources:  
	<ul>
      <li><a href="https://www.analyticsvidhya.com/blog/2017/03/tensorflow-understanding-tensors-and-graphs/
">Understanding Tensors and Graphs to get you started in Deep Learning</a></li>
      <li><a href="https://www.grc.nasa.gov/www/k-12/Numbers/Math/documents/Tensors_TM2002211716.pdf
">An Introduction to Tensors for Students
of Physics and Engineering</a></li>
      <li><a href="https://medium.com/@quantumsteinke/whats-the-difference-between-a-matrix-and-a-tensor-4505fbdc576c">What’s the difference between a matrix and a tensor?</a></li>
	  <li><a href="https://medium.com/@quantumsteinke/whats-the-difference-between-a-matrix-and-a-tensor-4505fbdc576c">What’s the difference between a matrix and a tensor?</a></li>
	  <li><a href="https://medium.com/@quantumsteinke/whats-the-difference-between-a-matrix-and-a-tensor-4505fbdc576c">What’s the difference between a matrix and a tensor?</a></li>
	  <li><a href="https://medium.com/@quantumsteinke/whats-the-difference-between-a-matrix-and-a-tensor-4505fbdc576c">What’s the difference between a matrix and a tensor?</a></li>
  	</ul> 
</p>
<p>If you have any question or feedback, please do reach out to me by commenting below.</p>


</div>
