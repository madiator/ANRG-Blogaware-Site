---
layout: post
title: "Reinforcement Learning"
date: 2012-06-30 16:23
comments: true
categories: ["reinforcement learning", "research", "dummies guide", "supervised learning", "unsupervised learning", "markov decision processes", "MDP", "multi-armed bandits"]
---

Even though I have used Markov Decision Processes and I know of the bandit problem framework, suddenly I realized that I could not relate these together with reinforcement learning. That meant that there was reading and learning in order. After spending some time on the wiki page and going nowhere, I turned to [this good tutorial](http://www.nbu.bg/cogs/events/2000/Readings/Petrov/rltutorial.pdf); and I decided to post what I learnt. The author has given a few good examples, but I wanted to formulate my own so that I can paint a better picture of reinforcement learning and where MDPs and bandit problems fit in the puzzle. 
<!-- more -->
## Supervised Learning
Consider a child, to whom you want to teach what is a bicycle using a set of images some of which contain bicycles and some do not. You start showing the child (toddler really) the pictures and tell her whether each image contains a bicycle or not. Eventually the child will learn to identify a bicycle because of your *supervision*. You have just completed supervised learning, and you could try to do something similar to a computer. 

## Reinforcement Learning
Now suppose you want to teach the child (she is much older now) how to ride a bicycle. One brutal approach is to put her on a bicycle and let her go on her own while merely tell her that she can either turn the handle bar to the left or to the right, or to shift her body to either side to prevent falling. She may fall a few times and recognize what to do and what not to do, and eventually after a few bruises would have learnt how to ride the bicycle. This is an example of *reinforcement learning*. For more understanding, read the following example from [the tutorial](http://www.nbu.bg/cogs/events/2000/Readings/Petrov/rltutorial.pdf):

> To provide the intuition behind reinforcement learning consider the problem of learning to ride a bicycle.
The goal given to the RL system is simply to ride the bicycle without falling over. In the first trial, the RL
system begins riding the bicycle and performs a series of actions that result in the bicycle being tilted 45
degrees to the right. At this point their are two actions possible: turn the handle bars left or turn them right.
The RL system turns the handle bars to the left and immediately crashes to the ground, thus receiving a
negative reinforcement. The RL system has just learned not to turn the handle bars left when tilted 45
degrees to the right. In the next trial the RL system performs a series of actions that again result in the
bicycle being tilted 45 degrees to the right. The RL system knows not to turn the handle bars to the left, so it
performs the only other possible action: turn right. It immediately crashes to the ground, again receiving a
strong negative reinforcement. At this point the RL system has not only learned that turning the handle bars
right or left when tilted 45 degrees to the right is bad, but that the "state" of being titled 45 degrees to the
right is bad. Again, the RL system begins another trial and performs a series of actions that result in the
bicycle being tilted 40 degrees to the right. Two actions are possible: turn right or turn left. The RL system
turns the handle bars left which results in the bicycle being tilted 45 degrees to the right, and ultimately
results in a strong negative reinforcement. The RL system has just learned not to turn the handle bars to the
left when titled 40 degrees to the right. By performing enough of these trial-and-error interactions with the
environment, the RL system will ultimately learn how to prevent the bicycle from ever falling over.

So as you can see here, in supervised learning, explicit input is provided whereas this is not the case with reinforcement learning and is a lot harder. Generally, a set of possible actions are specified and a notion of reward (reinforcement) is defined, and the goal is to maximize the cumulative reward by carefully choosing the actions. Falling down gets the child negative reward and probably being able to bike longer gets her positive reward. In a way, there is some input given to reinforcement learning and so it can be considered as a superset of supervised learning. 

## Unsupervised Learning
In case you are wondering whether learning the bicycle is an example of *unsupervised learning*, it is not. The goal of unsupervised learning is to find hidden patterns and structures in unlabeled data. Example: I give you four numbers {-101, -100, 100, 101}, can you find groups in this data? I am sure your first answer is to find two groups, the set of negative numbers and that of the positive ones. It was easy for you, but how does a computer do it? This is where unsupervised learning comes into pictures. Some of the tools that may be used for unsupervised learning are:

* [k-means](http://en.wikipedia.org/wiki/K-means)
* [Factor analysis](http://en.wikipedia.org/wiki/Factor_analysis)
* [Mixture models](http://en.wikipedia.org/wiki/Mixture_models)
* [Principal Component Analysis](http://en.wikipedia.org/wiki/Principal_component_analysis)
* [Independent Component Analysis](http://en.wikipedia.org/wiki/Independent_component_analysis)

If you let the child look at the photos may be she will be able to identify that there is a particular object (the bicycle) in a few photos.


Here is an excellent lecture by Andrew Ng of Stanford on reinforcement learning:
<iframe width="420" height="315" src="http://www.youtube.com/embed/RtxI449ZjSc" frameborder="0" allowfullscreen></iframe>


Some of the other examples that Andew Ng states for reinforcement learning:

* Training a dog by saying `good dog` and `bad dog`.
* Training a computer to play chess by assigning positive reward for winning and negative for losing. After many games, the hope is to get the computer win more often. 
* Training a helicopter by assigning positive reward to fly and negative reward if it crashes.


## MDPs & Bandits

One way of attacking a reinforcement learning problem is to take random actions at each point of time, completely ignoring the rewards. But in most cases, that is not going to take you anywhere. So in most cases, reinforcement learning problems are formulated as Markov Decision Processes (MDPs). I will talk about it in a bit more detail in a different post. 

Also, it turns out that the multi-armed bandit problem (again, it will be a separate post) is just a one state MDP where the actions correspond to the arms. The goal is to maximize the expected reward (or minimize the regret) while at each step picking one of the arms.

So there you go, I have tried to put together reinforcement learning, MDPs and bandit problems into the same context. If you find anything missing or have any other suggestions, please drop a comment! 