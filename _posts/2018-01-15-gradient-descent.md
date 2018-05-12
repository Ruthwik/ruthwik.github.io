---
layout: post
title: Gradient Descent Algorithm 
subtitle: Reach fast to Nadir.
published: true
categories: machinelearning
tags: [gradient descent,optimization , machine learning]

bigimg:
  - /img/gradientdescent/descentbg.jpg

---

<p>Gradient descent is an optimization algorithm for finding the minimum of a function. It takes steps proportional to the negative of the gradient to find the local minimum of a function. The following 3D figure shows an example of gradient descent. theta1 and theta0 are the two paramters. Gradient descent tries to find one of the local minima.</p>

<img src="/img/gradientdescent/gradient3d2.JPG" alt="gradient3d2"/>

> Gradients really become meaningful in multivarible functions, where the gradient is a vector of partial derivatives. With single variable functions, the gradient is a one dimensional vector with the slope as its single coordinate (so, not very different to the slope at all).

<p>The algorithm for gradient descent is shown as follows. The parameters are simultaneously updated.</p>

<img src="/img/gradientdescent/equation.jpg" alt="equation"/>

<p>The hyperparamter alpha is called learning rate. It is length of the step taken from every point to reach the local minima.</p>
> The first order derivative of a function gives the slope at that particular point.

<h3>Algorithm Explained</h3>
<p>
Let's look at an example and understand the gradient descent algorithm. Consider a linear equation as shown below. theta1 and theta0 are the two paramters. I will use <code>theta</code> wording instead of symbol.</p>
<img src="/img/gradientdescent/linearequation.JPG" alt="linearequation"/>

<p>There are many cost functions. In our case of linear equation, our purpose is to reduce the mean squared error between the hypothesis (h(x)) value and actual value.The cost function is shown as follows</p>

<img src="/img/gradientdescent/costfunction.JPG" alt="costfunction"/>

<p>
The following figure shows plot between J(theta1), theta1 and a tangent line (shown in red) that has a positive slope, and therefore has a positive derivative.    
</p>

<img src="/img/gradientdescent/positiveslope.JPG" alt="positiveslope"/>

<p>
In gradient descent the theta1 is updated as theta1, minus alpha times some positive number.The Alpha i.e the learning parameter, is always a positive number.So,the theta1 is updated as theta 1 minus something and therefore end up moving theta one to the left. This decreases theta one, and helps in moving towards the direction of the minimum. 
</p>
<img src="/img/gradientdescent/positiveslopeeqtn.JPG" alt="positiveslopeeqtn"/>

<p>Let's look at the negative slope tangent line. The following figure shows a tangent line (shown in red) that has a negative slope, and therefore has a negative derivative.</p>
<img src="/img/gradientdescent/negativeslope.JPG" alt="negativeslope"/>

<p>The theta 1 is updated as theta 1, minus alpha times some negative number. The Alpha i.e the learning parameter is always a positive number. So, the theta 1 is updated as theta 1 plus something and therefore end up moving theta one to the right. This increases theta one and helps in moving towards the direction of the minimum. </p>

<img src="/img/gradientdescent/negativeslopeeqtn.JPG" alt="negativeslopeeqtn"/>


<p>The learning parameter (alpha) value determines how fast or slow the gradient descent will be. If it is too small gradient descent will be slow. If it is too large then gradient descent will overshoot and may fail to converge.</p>

<h4>What if theta 1 is already at local minima?</h4>

<p>At the local optimum,the derivative will be equal to zero. So, the slope of this line will be equal to zero and thus this derivative term is equal to zero. If we are already at the local optimum it leaves theta 1 unchanged cause its updates as theta 1 equals theta 1. Therefore the  solution remains at the local optimum.</p>

<img src="/img/gradientdescent/thetaatlocal.JPG" alt="thetaatlocal"/>

<h4>How gradient descent finds local optima when there are many local optima?</h4>

<p>This happens in the non-convex functions</p>

> Convex function has no more than one minimum.Non-convex has with many local minima, but no global minima

<p>Let's first look at convex and non-convex functions.The following figure shows convex and non-convex function</p>

<img src="/img/gradientdescent/convex.jpg" alt="convex"/>

<p>In non-convex functions depending on the starting point, gradient descent will typically be attracted to the first local minima it encounters, so there is no guarantee it will a “good” local minima. In non-convex function shown above, there are a lot of local optima. And the optimization algorithms get stuck in a local optimum rather than find its way to a global optimum. How can we avoid this problem? In logistic regression, the initial cost function is a non-convex function. It is converted to convex function and this guarantees to find the global optimum.</p>


<p>
In a neural network, this intuition isn't actually correct. It turns out if we create a neural network, most points of zero gradients are not local optima. Instead, most points of zero gradients in a cost function are saddle points.
</p>
> In mathematics, a saddle point or minimax point is a point on the surface of the graph of a function where the slopes (derivatives) of orthogonal function components defining the surface become zero (a stationary point) but are not a local extremum on both axes.

<img src="/img/gradientdescent/saddle.JPG" alt="saddle"/>
<p>
 So, that's a point where the zero gradients, again. But informally, a function of very high dimensional space, if the gradient is zero, then in each direction it can either be a convex light function or a concave light function. And if we are in, say, a 10,000-dimensional space, then for it to be local optima, all 10,000 directions need to look like the convex function shown above. And so the chance of that happening is maybe very small. 
</p>

<p>
 Instead, you're much more likely to get some directions where the curve bends up like so, as well as some directions where the curve function is bending down rather than have them all bend upwards. So that's why in very high-dimensional spaces you're actually much more likely to run into a saddle point like that shown on the right, then the local optimum. That's why this point here, where the derivative is zero, that point is called a saddle point. </p>
<p>
If local optima aren't a problem, then what is a problem? It turns out that plateaus can really slow down learning.
</p>
> a plateau is a region where the derivative is close to zero for a long time.
> Self is not a Keyword. It is a coding convention.
<p> So if we are at a plateau, then gradient descents will move down the surface, and because the gradient is zero or near zero, the surface is quite flat. And maybe algorithm can actually take a very long time, to slowly find its way off the plateau due to a random perturbation of left or right.</p>
<p>
 The final takeaways about local optima are
 <ul>
	<li> It is unlikely to get stuck in bad local optima so long if we're training a reasonably large neural network. </li>
	<li> The plateaus can actually make learning pretty slow. And this problem can be solved using algorithms like momentum or RmsProp or Adam. </li>

</ul>
</p>

<p>I hope you liked this tutorial. Do check the following resources:  
	<ul>
      <li><a href="http://www.ugrad.math.ubc.ca/coursedoc/math100/notes/derivs/deriv5.html">So what is the derivative, after all?</a></li>
      <li><a href="https://www.coursera.org/learn/machine-learning">Machine learning course on Coursera by Andrew Ng</a></li>
      <li><a href="https://stats.stackexchange.com/questions/172900/can-gradient-descent-be-applied-to-non-convex-functions">Can gradient descent be applied to non-convex functions?</a></li>
	   <li><a href="https://ganguli-gang.stanford.edu/pdf/14.SaddlePoint.NIPS.pdf">Saddle Points</a></li>
	    <li><a href="https://datascience.stackexchange.com/questions/22853/local-minima-vs-saddle-points-in-deep-learning?noredirect=1&lq=1">local minima vs saddle points in deep learning</a></li>
		 <li><a href="https://www.analyticsvidhya.com/blog/2017/03/introduction-to-gradient-descent-algorithm-along-its-variants/">Introduction to Gradient Descent Algorithm (along with variants) in Machine Learning</a></li>
  	</ul> 
</p>

<p>If you have any question or feedback, please do reach out to me by commenting below.</p>

