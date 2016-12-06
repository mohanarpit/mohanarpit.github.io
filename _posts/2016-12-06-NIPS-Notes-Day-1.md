---
layout: post
title: NIPS Notes Day I
published: true
---

Since there's so much happening at NIPS on a daily basis, I thought it'll be
easier and better for me to table my thoughts and learnings in a post each day.

*Disclaimer: I'm a distributed systems engineer who's now interfacing with Machine learning teams.
This is why my theoretical understanding of Machine Learning is novice at best.*

## Tutorial I: Crowdsourcing beyond label generation

This was the first session by [Jenn Wortman](http://www.jennwv.com/).
It revolved around some salient points around managing the network.

Some of the direct applications of crowd sourcing are:
* Evaluating topic models. This is especially useful for data exploration and human interpretable summarization of text/audio/video.
* Human debugging of machine learning models. Useful to figure out the weak spots in the data pipeline.
If there's a huge error between human performance and machine performance, that's the step to focus on.
* Human clustering of data. The main idea here is to divide the dataset into multiple sections
and give them to multiple people with overlapping. The results are then aggregated using bayesian models.

Crowd-sourcing can also be effective while building Hybrid Intelligence Systems (human in the loop):
* A sample use-case is close captioning of audio in near realtime. The audio is split into multiple pieces
and distributed to a network of workers. As earlier, the results are collated and
aggregated before being displayed back to the user.
* Community sourced scheduling. [Project Cobi](http://projectcobi.com) gets humans to help the
machine identify constraints within a system. The machine then spits out a schedule based on those constraints.
* Information aggregation can be modelled as a stock market prediction of people's beliefs.
[Predictit](predictit.org) was doing this during the USA elections recently.

Social behaviour analysis of humans is a very interesting application of crowd sourcing.
In the past these studies have helped us identify better representations of numerals and find
the cost of bad online advertisements and spam.

### How to manage the crowd

#### Monetary Incentives
One of the first things to do while planning to pay workers is to pilot the task with
your team, colleagues & peers. This helps benchmark the difficulty & time of the task.
Once that is done, pay at least USA minimum wage.

**Do performance based payments work?**

Short answer: It depends. If the task is effort responsive (more time leads to better results)
then yes, else no. Unfortunately, it's not easy to figure out which task is effort responsive.

#### Intrinsic Motivation
Meaningful work leads to more quantity of work done by workers but not quality.

#### Communication Networks
It's incorrect to assume that crowd workers don't communicate. There are multiple external
forums that workers can use to communicate. Also, connected workers find work faster and also produce better results.

#### Best Practices
* Maintain good relationship with workers
* Respond to questions quickly
* Approve work quickly
* Avoid rejecting work unless extreme
* Pilot heavily with co-workers & collaborators
* Iterate the task N times
* Create clear instructions. Can include quiz questions if required.
* Create easy-to-use interface. Pilot this as well!
* Ask workers for feedback & bugs. Conduct exit surveys

## Tutorial II: Nuts & Bolts of AI Systems by [Andrew NG](www.andrewng.org/)

This was a very generic talk (surprisingly, with no maths). The focus was more on the process of developing
machine learning solutions rather than the actual maths behind it. An end-to-end deep learning
solution is one which follows the form: X ---[NN]---> Y. One of the ideas
that Andrew touched upon was that not all problems can be solved via end-to-end deep learning.
Those problems have to be broken down appropriately and then machine learning must be applied to it.
For example, recognizing a face via a security cameras is very hard because the background
keeps changing and so does the lighting. Instead, if we take the image, crop out everything but the face,
and then apply standard face recognition algorithms, the solution works much better.

*Definitions*:
* Difference b/w training & human error is **Avoidable bias**
* Difference b/w dev error & training error is **Variance**

A flow chart that should be followed while developing solutions is:

  A("If training error is high?")-- Y -->B("Try Bigger model, train longer, new model. (Bias)");
  A-- N -->C("Train-Dev error high?");
  C-- Y -->D("More data, regularization , new model (Variance)");
  C-- N -->E("Dev error high?");
  E-- Y -->F("Data synthesis, make data more similar (Domain adaptation - less common), New model architecture (Data mis-match problem)");
  E-- N -->G("Test set error high?");
  E-- Y -->H("More dev data (Overfitted dev data)");
  E-- N -->I("Done!");

For industrial applications, get the product manager to help the engineering team to
* Prioritize certain features
* Obtain dev & test set data
* Provide an evaluation metric for the model (Eg. F1 score, accuracy etc)

**Tips:**
* Read a lot of research papers because this is a fast moving field.
* Try to replicate results from other papers.
* Do the dirty work because that's what gives insights.

## Tutorial III: Generative Adversarial Networks
Generative Adversarial networks are those that try to generate data that fool the original
network into thinking that this is original data. It's like playing a game of cat & mouse.
This is a very new area of research and is still very green-field.

**Why do this?**

* Simulate possible futures for reinforcement learning
* Fill in missing inputs. Think semi-supervised learning.
* Multi modal outputs. If we want multiple possible outputs for a single input.

**Where is this useful?**

* Predicting the next frame of the video
* Upscale a single image
* Neural photo editing
* Image to Image translation

The salient properties of Generative Adversarial Networks are:
* Has latent code
* Asymptotically consistent (Unlike variational methods)
* No markov chains
* Produces the best samples. PixelCNN competes but unfortunately, there's no quantifiable way to compare this.

The basic terminology is that there is a Generator network that creates data. This data
is then fed into an actual model (Discriminator) whose job it is to mark these data points
as false and thereby re-inforce itself against such inputs.

**Tips & Tricks**
* Labels improve subjective sample quality.
* One sided label smoothing.
* Don’t smooth the negative labels. Basically smooth only the data and not the generator values. Doing this will cause the system to reinforce current generator behaviour.
* Use batch normalization.
* Balance the Generator & Discriminator. Usually the Discriminator wins which is a good thing.
* Use heuristic non-saturating cost

## Tutorial: Predictive Learning by [Yann](http://yann.lecun.com/)

Again, this talk was great in providing a lay of the land in the machine learning world.

Yann started out with the obstacles faced by AI today:
* Need to understand how the world works
* Large amount of background knowledge
* Need to perceive state of world
* Need to update and remember estimates of state of the world
* Need to reason and plan
* Intelligence & common sense = perception + predictive model + memory + reasoning & planning

He touched on various topics around Entity Recurrent Neural Networks, Unsupervised Learning & Adversarial Training
