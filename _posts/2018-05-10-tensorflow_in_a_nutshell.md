---
layout: post
title: TensorFlow in a Nutshell
subtitle: Quick start to TensorFlow.
published: true
categories: machinelearning
gh-repo: Ruthwik/StockPrediction
tags: [machine learning, TensorFlow, python]
bigimg:
  - /img/tensorflownutshell/tensorflowimage.jpg

---

<div class="text-justify">
<p>TensorFlow is a multipurpose Opensource software library for numerical computation using data flow graphs. It is originally developed by Google Brain Team to conduct deep neural networks research. TensorFlow is written in Python, C++ and CUDA. It provides stable Python API,C APIs and without backwards compatability gaurantee  C++, Go, Java, JavaScript and Swift. TensorFlow is applied in a wide variety of domains as well.The following figure shows how SketchRNN built using TensorFlow will complete your sketch in multiple ways.
</p>

<img src="/img/tensorflownutshell/magenta.gif" alt="magenta"/>
<p> <&emsp> Source: magenta.tensorflow.org </p>


<p> In this tutorial I	will cover the very	basics of TensorFlow. Deep learning will be covered in a different post. I will be using TensorFlow's Python API to explain.	

<h2>1. Installing TensorFlow</h2> 
<p>TensorFlow is a library and it can be installed like any other library using <code>pip</code> command.
<ul>
  <li>Install python 3.6 and above. Download from <a href="https://www.python.org/downloads//">here.</a></li>
  <li>Install Tensorflow <pre><code>pip3 install --upgrade tensorflow</code></pre></li>
</ul>
</p>
> Note: We will be using TensorFlow with CPU support only. If you have supporting GPU then please see these <a href="https://www.tensorflow.org/install/">instructions.</a>

<h3> 1.1 Importing TensorFlow</h3> 
<p>After installing, you can run the <code>import</code> statement to use TensorFlow library.
<script src="https://gist.github.com/Ruthwik/f1f93b42c1c47a3d85fa042d64d3d377.js"></script>
</p>


<h2>2. Tensors</h2> 
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

<h2>3. Computational graph</h2> 
<p>
TensorFlow internally represent the operations and performs its computation using a data flow graph (or computational graph). In other words
Tensorflow approaches series of computations as a flow of data through a graph with nodes being computation units and edges being flow of Tensors. 
</p>	
<img src="/img/tensorflownutshell/tf.gif" alt="magenta"/>
<p>
Nodes are the operations such as addition or subtraction and edges are the tensors.
It consists of two phases
<ul>
  <li>Build the graph: Here you define the Variables, Constants and Placeholders, and their relations.(define the mathematical operations on them)</li>
  <li>Execute the graph : Till now, all the variables and the computations applied. They are computed in this phase</li>
</ul>
</p>	
<img src="/img/tensorflownutshell/tf_graph.png" alt="magenta"/>

<h2>3.1. Build the graph <h2>

<h3> 3.1.1. Variables</h3> 
<p>
Let's see the official documentation definition
</p>
> A variable maintains state in the graph across calls to run(). You add a variable to the graph by constructing an instance of the class Variable.

> The Variable() constructor requires an initial value for the variable, which can be a Tensor of any type and shape. The initial value defines the type and shape of the variable. After construction, the type and shape of the variable are fixed. The value can be changed using one of the assign methods.

<p>
Variables can be created by tf.Variable().

<pre><code>tensorflow_var = tf.Variable(value, name="variable_name",dtype)</code></pre>

Most of the time you will want to create these variables as tensors of zeros, ones or random values:

<ul>
<li>tf.zeros() #creates a matrix full of zeros </li>
<li>tf.ones() #creates a matrix full of ones </li>
<li>tf.random_normal() #a matrix with random uniform values between an interval</li>
<li>tf.random_uniform() #random normally distributed numbers</li>
<li>tf.truncated_normal() 3same as random normal but doesn’t include any numbers more than 2 standard deviations.</li>
</ul>

<script src="https://gist.github.com/Ruthwik/8d780b7f42045dbbf5da28554baf3acb.js"></script>
</p>

<h3>3.1.2. Placeholders</h3> 

<p>
Placeholders are nodes whose values are fed in at execution time. In case of supervised learning the input-output pairs are fed in at execution time 
for training. In other words placeholder lets you inject external data to the computation graph.While declaring placeholders we only assign datatype and shape.

<pre><code>tensorflow_placeholder = tf.placeholder(dtype,shape=None,name=None)</code></pre>

</p>

<h3>3.1.3. Model</h3> 
<p>
Model is a mathematical function that maps the inputs to outputs using the model variables. For our example we will use 
a very simple linear model
<script src="https://gist.github.com/Ruthwik/d745f133c08270ec8233f71cfe76ba18.js"></script>

In the above line we defined our linear model in which we have defined two computation nodes <code>matmul</code> and <code>add</code>.
</p>

<h3>3.1.4. Loss Measure</h3> 
<p>
In machine learning, error is calculated as the difference between the actual output and the predicted output.
The function that is used to compute this error is called loss function. Different loss functions will give different 
errors. The performance of the model depends on the loss function. One of the most widely used is mean square error, where
loss function is calculated as the square of difference between actual value and predicted value.
Loss measure 
"# Mean squared error\n",
    "cost = tf.reduce_sum(tf.pow(pred-Y, 2))/(2*n_samples)\n",
</p>

<h3>3.1.5. Optimization Method</h3> 
<p>We will now divide the dataset into two parts for training and testing. Scikit provides <code>train_test_split(*arrays, **options)</code> to split the dataset.
By default, test_size value is set to 0.25 and train_size value is set to 0.75. We can change these values according to our needs.
<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>

tf_graph
<h2>3.2. Run the graph <h2>

<h2>3.2.1 Session</h2> 
<p>A Session object encapsulates the environment in which Operation objects are
executed, and Tensor objects are evaluated.

<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>

<h2>4. More things <h2>
<h3>4.1 DataTypes</h3> 
<p>Tensors have a data type in addition to shape and dimension. The following table shows the various datatypes available.
<img src="/img/tensorflownutshell/tensor_datatypes.JPG" alt="magenta"/>
</p>

<h3>4.2 Constants</h3> 
<p>Constant value cannot be changed When it is sure that value is not changed, tf.consant is used. It's initialization should be with a value, not with operation.
<script src="https://gist.github.com/Ruthwik/b00a1dc8def5956d5420272c1a33d116.js"></script>
</p>

<h2>5. TensorBoard</h2> 
<p>We will now divide the dataset into two parts for training and testing. Scikit provides <code>train_test_split(*arrays, **options)</code> to split the dataset.
By default, test_size value is set to 0.25 and train_size value is set to 0.75. We can change these values according to our needs.
<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>
<h3>5.1 Scope</h3>
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
	  <li><a href="https://becominghuman.ai/an-introduction-to-tensorflow-f4f31e3ea1c0">An Introduction to TensorFlow by Liu Songxiang</a></li>
	  <li><a href="https://medium.com/@quantumsteinke/whats-the-difference-between-a-matrix-and-a-tensor-4505fbdc576c">What’s the difference between a matrix and a tensor?</a></li>
	  <li><a href="https://medium.com/@quantumsteinke/whats-the-difference-between-a-matrix-and-a-tensor-4505fbdc576c">What’s the difference between a matrix and a tensor?</a></li>
  	</ul> 
</p>
<p>If you have any question or feedback, please do reach out to me by commenting below.</p>


</div>
