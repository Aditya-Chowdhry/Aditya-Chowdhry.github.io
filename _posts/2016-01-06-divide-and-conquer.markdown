---
title: "Divide And Conquer"
layout: post
date: 2016-01-06 17:00
tag:
- programming
- algorithms
- datastructures
- competitivecoding

image: #https://koppl.in/indigo/assets/images/jekyll-logo-light-solid.png
headerImage: true
projects: true
hidden: false # don't count this post in blog pagination
description: "How can divide and conquer approach can be applied to different coding problems?"
jemoji: ""
category: blog
author: adityachowdhry
externalLink: false
---

<!-- ![Screenshot](/assets/park-easy-screenshot.png)
 -->
In divide and conquer we solve a problem recursively, applying three steps at each level of recursion:

- **Divide** the problem into a a number of subproblems that are smaller instances of same problem.

- **Conquer** the subproblems by solving them recursively. If subproblems sizes are small enough, however, just solve the subproblems in a straightforward manner.

- **Combine** the solutions to the subproblems into the solution for the original problem.

One of the famous sorting algorithm Merge Sort is based on divide and conquer paradigm.

In this post I will focus on Merge Sort. The basic implementation of Merge Sort is :
![GIF](https://qph.ec.quoracdn.net/main-qimg-a29c0dd0186d1f8cef3c5ebdedf3e5a3)
Source: Wikipedia
{% highlight cpp %}
MergeSort(A, l,  r)
 
if l<r
	mid=(l + r)/2
	MergeSort(A,l,mid)   //Solve Left half
	MergeSort(A,mid+1,r) //Solve Right half
	Merge(A,l,mid,r)     //Merge left and right halves

{% endhighlight %}

{% highlight cpp %}
Merge(A,l,mid,r)
let temp[r-l+1] be a new array
i = l, j = mid+1
index = 0 
while i <= mid and j <= r
	if A[i] < A[j]
		temp[index] = A[i]
		i = i + 1
	else 
		temp[index] = A[j]
		j = j + 1
 
	index = index + 1
	
while i <= mid
	temp[index] = A[i]
	index = index + 1
	i = i + 1
 
while j <= r
	temp[index] = A[j]
	index = index + 1
	j = j + 1
p=0
for i = l to r
	A[i] = temp[p]
	p = p + 1

{% endhighlight %}

Implementation link: [Ideone.com](!http://ideone.com/cJCaLg)

Complexity : O(nlogn)

This was the implementation of  Merge Sort. Now moving forward, this technique of merge sort i.e divide and conquer can be helpful in solving some unique problems like:

### 1. Count inversions

***Probelm statement:***

*Inversion* Count for an array indicates – how far (or close) the array is from being sorted.  If array is already sorted then inversion count is 0.  If array is sorted in reverse order that inversion count is the maximum. Formally speaking, two elements a[i] and a[j] form an inversion if a[i] > a[j] and i < j
Example:
The sequence 2, 4, 1, 3, 5 has three inversions **(2, 1), (4, 1), (4, 3)**.

The naive solution O(n^2) is straight forward. Use two loops one i=1 to n-1 and other j=i+1 to n . If at any point A[i]>A[j] , increment count.

**How can you do it better?**

Think merge sort!.

How can you modify the merge operation to handle this problem?

What if we calculate the inversions when we put elements in a new array temp.?

**How?**

When we are merging arrays for example these two:

A={3,7,8,10} B={1,5,9,11,12}

We know two things in merge operation of merge sort that:

1. A and B are sorted individually.

2. Elements in A are on left side of all the elements in B.

So at any moment if any element in B is smaller than any element in A it is an inversion. There fore in this example.

1 is smaller than 3 , therefore inversion.

But how many inversions? As we know all elements in A are on left side to 1  and also as all elements after 3 will be larger than 3 so the inversions will be (3,1) , (7,1), (8,1), (10,1). Hence 4 inversions.

We can simply write this as **count += (mid+1-i)**.
{% highlight cpp %}
while(i<=mid && j<=r){
   if(A[i]<=A[j]){
     temp[index]=A[i];
     i++;	
   }else{
     temp[index]=A[j];
     j++;	
     cnt+=(mid+1-i);
  }
  index++;
} 
{% endhighlight %}
My implementation: [Ideone.com](http://ideone.com/INt2aw)<br>
Geeksforgeeks: [Count Inversions in an array | Set 1 (Using Merge Sort) - GeeksforGeeks](http://www.geeksforgeeks.org/counting-inversions/)

### 2. Count of smaller numbers after self

**Problem statement:** 


[Count of Smaller Numbers After Self | LeetCode OJ](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)  
You are given an integer array nums and you have to return a new counts array.
The counts array has the property where counts[i] is 
the number of smaller elements to the right of nums[i].

Example:
{% highlight cpp %}
Given nums = [5, 2, 6, 1]
 
To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
{% endhighlight %}

Return the array {% highlight cpp %} [2, 1, 1, 0] {% endhighlight %}

**Solution:**

This problem is same as above with only one modification that we need to make a count array.

For this it is necessary to preserve index also. Either you can create a structure or pair. For making pair I would suggest to go through C++ STL.

My solution: [Ideone.com](http://ideone.com/IWx2Rp)

### 3. Count of range sum

**Problem statement:**

Given an integer array nums, return the number of range sums that lie in *[lower, upper]* inclusive. Range sum S(i, j) is defined as the sum of the elements in A between indices i and j (i ≤ j), inclusive.

**Example:**
Given nums = [-2, 5, -1], lower = -2, upper = 2,
Return 3.
The three ranges are : [0, 0], [2, 2], [0, 2] and their respective sums are: -2, -1, 2.

The naive solution **O(n^2)** for this problem is trivial. How can you do it better?

First try to think about the naive solution, what would you need ?

A **prefix sum array**. Think about the solution using prefix sum array. If you are able to form O(n^2) solution then try to optimize it using Divide and Conquer approach.

Note: There are more approaches to this same problem.

This blog explains this thoroughly: [Count of Range Sum](http://52.20.106.37/count-of-range-sum/)

<center>Suggestions/Links are welcome.</center>