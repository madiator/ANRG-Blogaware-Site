---
layout: post
title: "Dummies Guide to Erasure Coding"
date: 2012-07-01 20:03
comments: true
categories: ["research", "erasure_coding", "dummies guide"]
published: true
---

If you read [this Wikipedia article on erasure coding](http://en.wikipedia.org/wiki/Erasure_code), you will be more prone to a headache than a person with migraine. Fortunately, there is help. Unfortunately, this article will be from the perspective of storage and not communication. This article is by no means rigorous, but should act as a 'dummies guide' and get you started. For example, if you are working on Hadoop and if you hear about people talking about erasure codes for Hadoop, this article will get you started. 

<!-- more -->

To begin with we will deal with what are called MDS codes. MDS stands for maximum distance separable. An MDS erasure code is generally represented as (n, k). 

The basic premise of erasure coding goes as follows:
> Take a file and split into k pieces and *code* into n pieces. Now, any k pieces can be used to get back the file. 

So here is the recipe:

* Take a file of size *M*. 
* Split the file into *k* chunks, each of the same size *M/k*.
* Now, apply the *(n, k)* code on these k chunks to get n chunks, each of the same size *M/k*.
* Now the effective size is *nM/k*. Thus the file is expanded *n/k* times. We need *n* to be greater than or equal to *k*, so *n/k* is at least 1. If *n* equals *k*, you have just split the file and there is no coding performed. 
* Any *k* chunks out of the *n* chunks can be used to get back the file. 

So this also means that the code can tolerate upto *(n - k)* erasures. 
The following figure shows this recipe being followed for a (4, 2) code.

![(4, 2) erasure code](http://photos.smahesh.com/photos/i-CKfxFLT/0/S/i-CKfxFLT-S.png)

Without really wondering how do actually add files, the following example illustrates one particular case of designing a (4, 2) code. 

![Simple example of a (4,2) code](http://photos.smahesh.com/photos/i-qMZPMh2/0/S/i-qMZPMh2-S.png)

Erasure codes were first designed to assist in detecting and correcting “problems” when sending data (through an unreliable channel). One of the famous examples of erasure codes are Reed Solomon codes. While erasure codes are also called as error correcting codes, there is a crucial difference between an error and an erasure. If I send ten bits and one bit flipped, an *error* has occurred, and I do not know where it has occurred. However, if I store ten blocks of a file into different nodes and one node dies, I know exactly which block I lost, and so I know where the *erasure* has happened. See the difference?

So thats all you need to know about erasure coding if you want to get started. Hopefully in a separate post, I will introduce other tools such as [Jerasure](http://web.eecs.utk.edu/~plank/plank/papers/CS-08-627.html), which can be used to implement erasure codes. 

Before signing off, let me now make a case for why it is a great idea to store files as coded blocks instead of complete files in a distributed storage system such as Hadoop. 

Lets say you have four computers (aka nodes) that you can use to store files. May be you are running Hadoop over these four nodes. Lets say that you have a file A that is two Hadoop-blocks in size. Clearly, instead of putting all the eggs in the same basket, you will want to spread it out and in this case, store the file twice by doing something like this:

![Uncoded storage](http://photos.smahesh.com/photos/i-xGXGQcN/0/M/i-xGXGQcN-M.png)

where X1 is the first block of file A and X2 the second. Another way is to store the coded blocks:

![Coded Storage](http://photos.smahesh.com/photos/i-cVW45Bz/0/M/i-cVW45Bz-M.png)

Now if you lose nodes 1 and 3, in the case when you store uncoded blocks, X1 is lost permanently, so the file A gets corrupted. Whereas in the case when you store coded blocks, even when those two nodes fail, it is possible to recover X1 and X2 and thus A from A2 and A4. This is because A2 = X2 and A4 = X1 + 2*X2. So one can solve these equations and get back X1 and X2! Neat, isn't it? One can now extend this to a more generic setting consisting of thousands of computers and may be millions of files (what better name to call other than a 'data center'?) and see that using erasure codes will help immensely. There are more nuances of the problem that I will not undertake here, and there is something called a repair problem, and if interested, please take a look at [Prof. Alex Dimakis's work](http://www-bcf.usc.edu/~dimakis/). 