---
layout: post
title: NIPS Notes Day II
published: true
---
This post is a continuation of a series. You can view the first part [here](NIPS-Notes-Day-1).

## Keynote I: Intelligent Biosphere
The day started with a very beautiful presentation by [Dr. Drew Purves](http://drewpurves.com)
It was a very high level talk where he urged folks to derive inspiration from nature while building
models. One of the most interesting ideas he proposed was the fact that from an evolutionary
front, each organism may not necessarily compete with another for resources. This is because
they operate at different niches (think of soil at 10m, 50m, 100m depth). Every once in a while
a species may create a new niche to reduce competition. Humans are excellent at that.

The keynote was followed by a number of oral paper presentations (some that I didn't
really understand from the get-go).

## Session I: Value Iteration Networks
The slides for this talk can be found [here](http://www.cs.columbia.edu/~blei/talks/2016_NIPS_VI_tutorial.pdf)

## Session II: Interactive Clustering
Unlike supervised learning, for clustering, the goal is not very clear. This is because
there can be various ways to cluster data.

**Challenges**:

* We don’t have enough domain knowledge. This problem is called under-specificity.
* High computational complexity. Clustering requires a lot of computation power.
* Optimizing k-means/k-median is NP Hard.

Some of the ways to acquire domain knowledge and solve the under-specificity problem is:

* Trial & error.
* Offline models such as
  * Constrained Clustering
  * Demonstration based clustering
* Interactive Clustering

The approach is fairly straight-forward. The learning agent asks an expert/human the question
"*Does point x1 & x2 lie within the same cluster?*". This natural form of query is common
during record de-duplication & assisted troubleshooting. Asking such questions reduces the
computational complexity of the problem as well.

The algorithm is simple.
* Pick a random point and assume that be to be the center.
* Query the expert uniformly till we have enough points from 1 cluster.
* Prune all the points from that cluster and don't take them into consideration again.
* Binary search to figure out the radius of that cluster

Based on the distance between x1 & x2, come up with a radius of the cluster such that
x2 is G times away from the center of the center. That way, we can simply binary search our way through
the problem to find the actual radius R of the cluster.

The beauty of this solution is that it works on un-balanced clusters and also doesn't need to know
either the number of clusters or their sizes. Unfortunately, it doesn't handle noise very well.

## Session III: Speeding Up k-means
This paper proposed a 1000x speed up of k-means calculation by performing some very simple steps
for seeding and then fine-tuning the selection.

The algorithm goes as follows.
1. Pick a random point as the center of the cluster.
2. The next point is picked via D^2 sampling and construct a Markov chain. So a new candidate y1
is picked according to some function q(x) where x is the first point.
3. According to some probability, we decide if the Markov chain shifts to y1 or remains at x1.
This is repeated M times to create a Markov chain of length M. The last point of this
chain is returned as the next cluster center.

The advantages of this approach are:
* It's biased towards points away from the previous cluster center thereby ensuring complete coverage of he dataset.
* Faster than K-MC2

Better still, the code is available [here](olivierbachem.ch) and as a pip module via

`pip install kmc2`

## Keynote II: Engineering Principles from Stable Brains by [Saket Navlakha](www.snl.salk.edu/~navlakha)
This was in some senses an extension to the earlier keynote on getting inspired by nature.
The speaker took up 2 inspirations from nature. The first was the networks within our brains
while the other was how flies decide what's food & what's not.

Let's look at the first example. Brains start out with a hyper-connected network of neurons.
Over a period of time, only the pathways that get used a lot continue to remain while the rest are destroyed.
This seems to be less energy efficient but it leads to much more efficient networks. This same principle
could be applied to wireless network design. The rate at which the pruning happens also plays a big factor.
A decreasing rate of pruning causes a sharp drop-off initially but then a long tail allows the network to optimize
the network slowly. The draw-back is that a decision must be made initially but leads to be better networks overall.

The other example looked at how flies take decisions on what's interesting and what's not. This is done via
locality sensitive hashing. All objects that smell similar are interesting. Therefore they must be in the same bucket.
The way this is done is that while firing neurons on the next layer, only certain firings above a certain confidence level
are taken. The rest weights are discarded. This is a "winner takes all" model. Basically the neurons fire and send a signal to APL.
The APL feeds back and shuts down the neutrons that aren’t required. This allows us to maintain locality & relative distance while
still cutting down on computation. Such sparse data points are also encountered in Hadoop & Big Data as well.

## Session IV: AI for Game Theory

## Session V: Using fast weights to attend to the recent past

## Session VI: Phased LSTM
Generally LSTMs perform badly when there are long conversations with more than 10K timesteps.
Also, if the frequency of the data is irregular (sensor data) then also LSTMs are a sub-optimal solution.
The proposed solution has an out-of-sync sleep-wake rhythms along with an explicit time gated input.
This allows the system to store a lot more memory.

The complete paper can be read [here](http://papers.nips.cc/paper/6310-phased-lstm-accelerating-recurrent-network-training-for-long-or-event-based-sequences).

If you do find these notes interesting or find a mistake, do leave a comment or ping me on [twitter](https://twitter.com/mohanarpit)
