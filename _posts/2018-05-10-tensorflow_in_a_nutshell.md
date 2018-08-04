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

<h3>Installing TensorFlow</h3> 
<p>TensorFlow is a library and it can be installed like any other library using <code>pip</code> command.
<ul>
  <li>Install python 3.6 and above. Download from <a href="https://www.python.org/downloads//">here.</a></p></li>
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

> Tensors are geometric objects that describe linear relations between geometric vectors, scalars, and other tensors. Elementary examples of such relations include the dot product, the cross product, and linear maps. Geometric vectors, often used in physics and engineering applications, and scalars themselves are also tensors.

<img src="/img/tensorflownutshell/tensors.jpg" alt="magenta"/>

<p>
A Tensor has the following properties:
</p> 
<img src="/img/tensorflownutshell/tensor_rank.jpg" alt="magenta"/>

<p>
The rank of a tensor is its number of dimensions.The shape of a tensor is the number of elements in each dimension
</p>
| Rank        | Shape           | Dimension number  | Example  |
| ------------- |:-------------:| -----:| -----:|
| 0      | [] | 	0-D | A 0-D tensor. A scalar. |
| 1      | [D0] | 	1-D | A 1-D tensor with shape [5]. |
| 2      | [D0, D1] | 	2-D | A 2-D tensor with shape [3, 4].|
| 3      | [D0, D1, D2] | 	3-D | A 3-D tensor with shape [1, 4, 3]. |
| n      | [D0, D1, ... Dn-1] | 	n-D | A tensor with shape [D0, D1, ... Dn-1]. |

<img src="/img/tensorflownutshell/tensor_scalar_vector.jpg" alt="magenta"/>
<p>

</p>


<p>Now, lets see the steps for preparing the dataset for Linear Regression model training. 
Firstly, we import the stock dataset file using pandas library method <code>pd.read_csv</code> to pandas dataframe. 
Second, converting the date into numeric value using time and date python library. We can also convert date into different columns like day,month and year
 but for our simplicity of one feature let's just convert into numeric value. 
 The third one is to convert the pandas dateframe into numpy array using <code>np.array()</code>. The linear model of scikit accepts only numpy array.
 The last one is to reshape the numpy arrays to n X 1 shape. The <code>reshape()</code> method will reshape the features so that it will be feed to scikit library. 
<script src="https://gist.github.com/Ruthwik/1f6153eef33cf30a20693ce1101a80d7.js"></script>
</p>	

<p>We will now divide the dataset into two parts for training and testing. Scikit provides <code>train_test_split(*arrays, **options)</code> to split the dataset.
By default, test_size value is set to 0.25 and train_size value is set to 0.75. We can change these values according to our needs.
<script src="https://gist.github.com/Ruthwik/c5e09ec6b1ddf56873847071dbaff058.js"></script>
</p>

<p>Our next step is to visualize the dataset for data insights. Although our dataset is a simple one, it is a good practise to visualize the data.Using Matplotlib we can plot the graph</p>
<img src="/img/stockdataset_visualize.png" alt="date vs. price"/>

<p>Linear Regression implementation is pretty straight forward in scikit. 
Two lines of code is all that is required. First line will fit the the training data into the linear regression model. 
The second line is to use the trained model to predict.Now we have a trained Linear Regression model. We are now able to make predictions on unseen data
<script src="https://gist.github.com/Ruthwik/d93ddba6dedda504789796718967901d.js"></script>
</p>
<p>
How would we know whether our model is good enough? For that we calculate coefficient of determination.
<i>R<sup>2</sup> is a statistic that will give some information about the goodness of fit of a model. 
In regression, the R<sup>2</sup>  coefficient of determination is a statistical measure of how well the regression line approximates the real data points. 
An R<sup>2</sup> of 1 indicates that the regression line perfectly fits the data.</i>. <code>linear_model_.score(X, y)</code> gives us the score. 
Our training data score is 0.785 and testing data score is 0.787. Training and testing scores will give us information about model overfitting and underfitting.
If the model performs well during training (training score) and underperforms during testing (testing score) then the model is <i>overfiting</i>. If the model doesn't perform 
well during training or testing then the model is <i>underfitting</i>. Our model is performing decently well.
<script src="https://gist.github.com/Ruthwik/ff7c9a36a21461955a0c24ba76eec3c8.js"></script>
</p>
<p>
Now, let's plot the trained Linear Regression model. The plot below also showing the prices of apple stock and the learned regression line.
<script src="https://gist.github.com/Ruthwik/3c274894527354c8948a19aac44d84aa.js"></script>

<img src="/img/trained_model.png" alt="date vs. price on trained model"/>
</p>
<p>
Before concluding let's predict the price of the apple stock on a given day. 
<script src="https://gist.github.com/Ruthwik/331de409f77d68147353978fbbc08844.js"></script>
</p>
<p>I hope you liked this tutorial. You can find the complete code on my github <a href="https://github.com/Ruthwik/StockPrediction">StockPrediction</a>. 
If you want to learn more about maths behind Linear Regression or ML in general, do check the following resources:  
	<ul>
      <li><a href="https://www.khanacademy.org/math/probability/regression/regression-correlation/v/regression-line-example">Linear Regression on Khan Academy</a></li>
      <li><a href="https://www.coursera.org/learn/machine-learning">Machine learning course on Coursera by Andrew Ng</a></li>
      <li><a href="http://eu.wiley.com/WileyCDA/WileyTitle/productCd-0470542810.html">Introduction to Linear Regression Analysis by Douglas Montgomery, Elizabeth A. Peck, and G. Geoffrey Vining</a></li>
  	</ul> 
</p>
<p>If you have any question or feedback, please do reach out to me by commenting below.</p>


</div>
