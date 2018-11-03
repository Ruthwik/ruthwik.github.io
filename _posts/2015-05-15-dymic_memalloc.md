---
layout: post
title: Dynamic Memory allocation in C and C++
subtitle: Save your memory.
published: true
categories: other
tags: [C, C++, Dynamic Memory allocation of 2D array in C++, Dynamic Memory allocation.]

bigimg:
  - /img/oldblog/cpp.jpg

---

## Dynamic Memory allocation in C
<p>   First let us look into how the memory is organized. The memory is mainly divided into stack, heap and permanent storage area. The Stack is used to store local variables. Global variables, program instructions and static variables are stored in the permanent storage area. Our main concern is heap which is free memory available, allocated dynamically using some standard library functions. </p>

<p>In C, the two key dynamic memory functions are malloc() and free().The prototype for malloc looks like  <code>void *malloc(size_t size)</code> and for free it looks like <code>void free(void *pointer)</code>
 </p>

<p>Here is an example to illustrate the use of these functions:</p>    
<p> The static way of defining an array</p>    
```c++
	int a[100];
	a[10] = 25;
```

<p>The dynamic way of defining an array</p>   
```c++ 

	int *p;
	p = malloc(100 * sizeof(int));
	*(pointer+10) = 25;

```
<p>When the array is no longer needed, it is deallocated using free function</p>  
```c++

	free(p); 
	p = NULL;

```  
<p>The assigning of NULL to pointer 'p' is optional, but it is done in order to avoid <a href="https://en.wikipedia.org/wiki/Dangling_pointer">dangling pointer problem</a>
</p>


<p>For more understanding refer <a href="https://www.studytonight.com/c/dynamic-memory-allocation-in-c.php">Dynamic memory allocation in c</a>.</p>

## Dynamic Memory allocation in C++

<p> C++ provides two operators new and delete for dynamic memory allocation.</p>
<p>The following syntax shows the use of new operator in various ways</p>
```c++
	variable = new typename;
	variable = new type(initializer);   //includes initialization
	array = new type [size];    //array of objects
	
```
<p>The memory is de-allocated using delete operator as shown:</p>
```c++
	delete variable;
	delete[] array;

```

<p>Here is an example to create a dynamic 1D array:</p>
```c++
	int *p;
	pointer = new int[100];
	pointer[10] = 25; 
```
<p>The pointer p is deallocated using delete:</p>
```c++
	delete[] p;
	p = NULL;
```
> C++ provides another option for dynamic memory allocation using the Standard Template Library.

## Dynamic Memory allocation of 2D array in C++
<p>  Allocating memory for 2D array is not straight forward like normal 1D array. A dynamic 2D array is an array of pointers to arrays. </p>
<p>The steps used to create a dynamic 2D array are:</p>
```c++

	int** a = new int*[row_size];  

	for(int i = 0; i < row_size; ++i){
		a[i] = new int[column_size];
		}
```
<figure>
<img src="/img/oldblog/dyamicmemory.jpg" alt="ns"/>
  <figcaption>Figure 1.</figcaption>
</figure>

<p>First step creates 1D dynamic array(which is array of pointers) and in second step creates the column of the array. Figure 1 gives a clear idea.</p>
<p>Deallocating dynamic 2D array:</p>
```c++
	for(int i = 0; i < row_size; ++i) {
		delete [] a[i];
		}
		
	delete [] a;
```
<p>Here is an example for creating and deleting dynamic 2D array with 4 rows and 5 columns (i.e a[4][5]):</p>

```c++
	int** a = new int*[4];
	for(int i = 0; i < 4; ++i){
		ary[i] = new int[5];
		}

	for(int i = 0; i < 4; ++i) {
		delete [] a[i];
		}
		
	delete [] a;
```
 
<p>This article is taken from my old blog.</p>


