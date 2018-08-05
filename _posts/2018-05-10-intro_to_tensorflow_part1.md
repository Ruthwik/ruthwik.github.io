---
layout: post
title: Introduction to TensorFlow - Part 1
subtitle: kick start to TensorFlow.
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
<p> Source: magenta.tensorflow.org </p>


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

> Tensors are geometric objects that describe linear relations between geometric vectors, scalars, and other tensors.Elementary examples of such relations include the dot product, the cross product, and linear maps. Geometric vectors, often used in physics and engineering applications, and scalars themselves are also tensors.

<img src="/img/tensorflownutshell/tensors.png" alt="tensors" width="451" height="406/>

<p>
A Tensor has the following properties:
</p> 
<img src="/img/tensorflownutshell/tensor_rank.jpg" alt="tensor_rank"/>
<p> Source: slideshare.net </p> 
<p>
The rank of a tensor is its number of dimensions.The shape of a tensor is the number of elements in each dimension
</p>

<img src="/img/tensorflownutshell/shape.jpg" alt="shape"/>

<p>
The following image gives a better intuition about Tensors.
</p>
<img src="/img/tensorflownutshell/tensor_scalar_vector.jpg" alt="tensor_scalar_vector"/>
<p> Source: google.com </p> 
<p>
In simple terms Tensors are called as multidimenional arrays.
</p>

<h2>3. Computational graph</h2> 
<p>
TensorFlow internally represent the operations and performs its computation using a data flow graph (or computational graph). In other words
Tensorflow approaches series of computations as a flow of data through a graph with nodes being computation units and edges being flow of Tensors. 
</p>	
<img src="/img/tensorflownutshell/tf.gif" alt="magenta"/>
<p> Source: tensorflow.org </p>
<p>
Nodes are the operations such as addition or subtraction and edges are the tensors.
It consists of two phases
<ul>
  <li><code>Build the graph</code>: Here you define the Variables, Constants and Placeholders, and their relations.(define the mathematical operations on them)</li>
  <li><code>Execute the graph</code>: Till now, all the variables and the computations applied. They are computed in this phase</li>
</ul>
</p>	
<img src="/img/tensorflownutshell/tf_graph.png" alt="magenta"/>
<p> Source: google.com </p> 


<h2>3.1. Build the graph <h2>

<h3> 3.1.1. Variables</h3> 
<p>
Let's see the official documentation definition
</p>
> A variable maintains state in the graph across calls to run(). You add a variable to the graph by constructing an instance of the class Variable.The Variable() constructor requires an initial value for the variable, which can be a Tensor of any type and shape. The initial value defines the type and shape of the variable. After construction, the type and shape of the variable are fixed. The value can be changed using one of the assign methods.

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
</p>
<script src="https://gist.github.com/Ruthwik/8d780b7f42045dbbf5da28554baf3acb.js"></script>


<h3>3.1.2. Placeholders</h3> 

<p>
Placeholders are nodes whose values are fed in at execution time. In case of supervised learning the input-output pairs are fed in at execution time 
for training. In other words placeholder lets you inject external data to the computation graph.While declaring placeholders we only assign datatype and shape.

<pre><code>tensorflow_placeholder = tf.placeholder(dtype,shape=None,name=None)</code></pre>

</p>
<script src="https://gist.github.com/Ruthwik/d4c5f30329aff71722d32ecdb7cba825.js"></script>

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
loss function is calculated as the square of difference between actual value and predicted value which is divided by total samples.

<script src="https://gist.github.com/Ruthwik/5559286bb9aa1ef0032ac115acbb1173.js"></script>


</p>

<h3>3.1.5. Optimization Method</h3> 
<p>Optimization Algorithms are used to update weights and biases i.e. the internal parameters of a model to reduce the error. We are going to use Gradient Descent optimizer to optimize our model parameters. We create our optimizer object <code>tf.train.AdamOptimizer</code> and add an optimization operation on the graph by calling minimize method on the optimizer object. Please see my post on Gradient Descent Algorithm to know about how an optimization algorithm works.
<script src="https://gist.github.com/Ruthwik/33353b66be2aa378516cadbe7b6256f9.js"></script>

minimize(cost) does two things:

<ul>
<li>Computes the gradient of our argument (loss node) with respect to to all the variables (weights and biases). </li>
<li> Applies gradient updates to all those variables.</li>
</ul>
</p>

<h2>3.2. Run the graph </h2>

<p>
We have constructed the necessary componenets of the computation graph. The next step is to execute it.
</p>

<h3>3.2.1 Session</h3> 
<p>A Session object encapsulates the environment in which operation objects are
executed, and Tensor objects are evaluated.
To execute the graph, we must initialize a Session object, and call its run method.

</p>
<h4>Create Session object</h4> 
<p>
There are two ways to create the session object as shown below.
<script src="https://gist.github.com/Ruthwik/bd2c2c024adec3e73ff878818b4ed763.js"></script>
</p>
<h4>Initialize the variables</h4> 
<p>
We need to initialize the variables as we only assign real values to the variables once we are in a runtime 
i.e. after a session has been created.
<script src="https://gist.github.com/Ruthwik/e089fab9f9beeadb67882c0163337b56.js"></script>
</p>

<h4>Run the method of Session object</h4> 
<p>
The run method of Session object evaluates the output of a node of the graph
</p>
<script src="https://gist.github.com/Ruthwik/18b50facd7cf295d84dea3974016aa9c.js"></script>

<h2>4. More Information<h2>
<h3>4.1 DataTypes</h3> 
<p>Tensors have a data type in addition to shape and dimension. 
The following table shows the various datatypes available.
</p>

<img src="/img/tensorflownutshell/tensor_datatypes.JPG" alt="tensor_datatypes"/>


<h3>4.2 Constants</h3> 
<p>Constant value cannot be changed once create. When it is sure that value will not change, tf.consant is used. It's initialization should be with a value, not with operation.
<script src="https://gist.github.com/Ruthwik/b00a1dc8def5956d5420272c1a33d116.js"></script>
</p>


<h2>5. Stitching</h2>

<p>
Before concluding let's predict the price of the apple stock on a given day.  We will use all the code snippets and use them to complete the stock
prediction script.
<script src="https://gist.github.com/Ruthwik/5ce74992f84e3617a4f51d4f22a3b3de.js"></script>
</p>
<p>I hope you liked this tutorial. You can find the complete code on my github <a href="">Linear Regression using TensorFlow</a>. 

I have used the following references and sometimes used the same explanation. Do check the following resources for more understanding.
 
	<ul>
      <li><a href="https://www.analyticsvidhya.com/blog/2017/03/tensorflow-understanding-tensors-and-graphs/
">Understanding Tensors and Graphs to get you started in Deep Learning</a></li>
      <li><a href="https://www.grc.nasa.gov/www/k-12/Numbers/Math/documents/Tensors_TM2002211716.pdf
">An Introduction to Tensors for Students
of Physics and Engineering</a></li>
      <li><a href="https://medium.com/@quantumsteinke/whats-the-difference-between-a-matrix-and-a-tensor-4505fbdc576c">What’s the difference between a matrix and a tensor?</a></li>
	  <li><a href="https://becominghuman.ai/an-introduction-to-tensorflow-f4f31e3ea1c0">An Introduction to TensorFlow by Liu Songxiang</a></li>
	  <li><a href="https://medium.com/@camrongodbout/tensorflow-in-a-nutshell-part-one-basics-3f4403709c9d">TensorFlow in a Nutshell — Part One: Basics by Camron Godbout</a></li>
	  <li><a href="https://medium.com/data-science-group-iitr/loss-functions-and-optimization-algorithms-demystified-bb92daff331c">Loss Functions and Optimization Algorithms. Demystified. by Apoorva Agrawal</a></li>
  	</ul> 
</p>
<p>If you have any question or feedback, please do reach out to me by commenting below.</p>


</div>
