---
layout: post
title: Multiple Inheritance in C++
subtitle: Best way to inherit.
published: true
categories: other
tags: [C++, Diamond problem, explicit scoping., Inheritance, Multiple Inheritance, Virtual Base class]

bigimg:
  - /img/oldblog/inheritance.jpg

---

## Introduction

<p> In multiple inheritance a derived class inherits from more than one class.The following figure gives an idea. </p>

<figure>
<img src="/img/oldblog/multi.jpg" alt="ns"/>
  <figcaption>Figure 1</figcaption>
</figure>

<p> In Figure 1 class D is the derived class and B,C are base classes for it.</p>

<p>Consider the following program:</p>

## Problems with Multiple Inheritance
<script src="https://gist.github.com/Ruthwik/10b2bc123c65c1dd8aaa72a881e4b0c5.js"></script>


<p>We will get an error: request for member 'display' is ambiguous.</p>

<p>Why this happens? Think!!!</p>
<p>Let's look how the compiler evaluates the above program: 

After creating an object of type D when we call the function display using that object the compiler searches for display function in class D. As the compiler cannot find it then looks to see if any of the base classes have a function named display().

The problem is that 'dobject' actually contains two display() functions: one inherited from class B, and one inherited from class C. Therefore compiler cannot choose between the two and the function call is ambiguous, and will receive a compiler error.</p>
<p>How to solve this problem?</p>

<p>One way is to explicitly mention from which class the method has to be derived. This is known as <b>explicit scoping.</b></p>
```c++

	dobject.B::display(dobject.d_var);
	
```
<p>And the output is:</p>
```
	Called from B and value is 40
```

## Diamond Problem

<p>Let's complicate things a bit more. Now have a look at the following figure:</p>    

<figure>
<img src="/img/oldblog/multiinherit.jpg" alt="ns"/>
  <figcaption>Figure 2</figcaption>
</figure>


<p>   If the function display is derived from A the program looks like this:</p>
<script src="https://gist.github.com/Ruthwik/9aab7689d7a37a12b5ce6ee716e84920.js"></script>

<p>The same problem as in the case of multiple inheritances exists and also adds more problems to it.

The compiler doesn't know whether it should have one or two copies of A and how to resolve such ambiguous references. While these problems can be solved using explicit scoping but the maintenance overhead increases.</p>

<p>If we create object of type D then by default compiler ends up creating two copies of class A. As shown in the figure 3.</p>
<figure>
<img src="/img/oldblog/multiinheritance.jpg" alt="ns"/>
  <figcaption>Figure 3</figcaption>
</figure>

<p>Most of the times we want the compiler to create only one copy of class A.</p>
<p>Is it possible?</p>
<p>Yes, it is possible with the help of <b>virtual base classes</b>.</p>

<p>So let's make some changes to the code and make it work.</p>
<script src="https://gist.github.com/Ruthwik/79c8027228b30739ca4465bd697234d5.js"></script>

<p> And the Output looks like: </p>
```
	Called from A and value is 40
```
<p>Here Class A is constructed only once. Before finishing this topic there are few points to be remembered.</p>
<p><b>First</b> virtual base classes are created before non-virtual base classes, which ensures all bases get created before their derived classes. </p>

<p><b>Second</b>, note that the constructors of Classes B and C still have calls to the A's constructor. If we are creating an instance of D, these constructor calls are simply ignored because D is responsible for creating the A, not B or C. However, if we were to create an instance of B or C, the virtual keyword is ignored, those constructor calls would be used, and normal inheritance rules apply.</p>

<p><b>Third</b>, if a class inherits one or more classes that have virtual parents, the most derived class is responsible for constructing the virtual base class.</p>



 
<p>This article is taken from my old blog.</p>


