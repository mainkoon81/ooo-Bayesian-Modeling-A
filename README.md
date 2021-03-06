# What is PGM ?
: It's a probabilistic model for which a graph expresses the **conditional dependence structure** between random variables.

: Understanding what makes **`Conditional Independence`** b/w variables helps us explain some uncertainty reasoning. If x, y are conditionally independent on `z`, then
 - P(x | y,`z`) = P(x|`z`)
 - P(x,y | `z`) = P(x|`z`) * P(y|`z`)
 - P(x, y, z) ∝ ϕ(x,`z`) * ϕ(y,`z`) ????

: PGM allows a tractable inference!

<img src="https://user-images.githubusercontent.com/31917400/92264526-4702cf80-eed6-11ea-97e7-72618640aa8d.jpg" />
<img src="https://user-images.githubusercontent.com/31917400/52655869-1a025c80-2eed-11e9-82ba-1fdea931596f.jpg" />

 - Let's say we want to classify data points that are independent of each other(for example, given an image, predict whether it contains a cat or a dog), but See `I`, `like`, `machine`, `learning`... Problem here is that `learning` could be a noun or a verb depending on its context. Probabilistic graphical model is a powerful framework which can be used to learn such models with **dependency**.
 - PGM consists of a graph structure. Each `node` of the graph is associated with a **random variable**, and the `edge` in the graph are used to encode **relations** between the random variables. Because of the way the graph structure encodes the `parameterization` of the probability distribution,
   - It gives us an intuitive and compact data structure for capturing **high dimensional probability distributions**. 
   - It gives us a suite of methods for **efficient reasoning**, using general purpose algorithms
   - It gives us a **reduction in the number of parameters** thus **`we can represent these high-dimensional probability distribution efficiently using a very small number of parameters`**. 
     - Reduce factors down. In the graphic, Drop the arrows as many as possible based on conditional independence!
     <img src="https://user-images.githubusercontent.com/31917400/69966964-58feae80-150f-11ea-852b-1b4efa485e71.jpg" />

Depending on whether the graph is **directed or undirected**, we can classify graphical modes into two categories.
 - ## [a] Bayesian networks
   - Definition: Given X~P(X), and as an ordered DAG, we build a `joint`: where Each variable X_i should be **independent** each other but if some of them are hoplelessly dependent, and we can make them **conditionally independent**, then... 
     <img src="https://user-images.githubusercontent.com/31917400/69970023-6880f600-1515-11ea-82e4-ed9e176cc946.jpg" />

   - It defines probability distributions over **graphs of random variables**. Instead of enumerating all possibilities of combinations of multiple random variables, it defines probability distributions that are inherent to each individual node. The definition of this **`joint distribution`** by using such factors has one great advantage: `we can reduce the number of probability values(parameters) required`.
     <img src="https://user-images.githubusercontent.com/31917400/67589802-3ed3f280-f751-11e9-8de9-a5eca09adb8b.jpg" />     
   
   - # Key: **Factorization of `joint distribution`**
   - `P(a,b,c)` = P(**a|b**,c)`P(b,c)` = P(a|b,c)P(b|c)P(c)
   - `P(a,b,c)` = P(**a,b**|c)`P(c)`
     - P(**a|b**,`C`): it's mainly a `conditional` = **P(a,b)/P(b)** = P(a,b|`C`)/P(b|`C`) 
     - P(**a,b**|`C`): it's mainly a `joint`= **P(a|b)P(b)** = P(a|b,`C`) P(b|`C`) 
     - If `|` is already present, then simply add the extra `C`, otherwise add `|` then add `C`. 
   - Example
     - Directed PGM & Bayesian OLS Regression
       <img src="https://user-images.githubusercontent.com/31917400/69980377-07aee900-1528-11ea-8fad-d6758bf79b65.jpg" />

     - Directed PGM & Bayesian NaiveBayes Classification
       <img src="https://user-images.githubusercontent.com/31917400/93786998-da9f0480-fc27-11ea-8f9d-df4d3dc7e5d1.jpg" />

 - ## [b] Markov networks
   - T.B.D


---------------------------------------------------------------------------------------------------------
# (A) Representation
## A1> Bayesian Network Intro
<img src="https://user-images.githubusercontent.com/31917400/93762637-e11d8400-fc07-11ea-936a-af4382c997bf.jpg" />

> # so what?
Bayesian networks allow to model causal relationships between variables, compensating the lack of information provided by data. BN can be used for a wide range of tasks including prediction, anomaly detection, diagnostics, automated insight, reasoning, time series prediction and decision making under uncertainty. It uses a `directed graph` as the intrinsic representation. Bayesian Network is a Directed Acyclic Graph(DAG) whose nodes represent the random variables X1, X2, ... It represents a `joint distribution`(via the chainRule) for Bayesian Networks. Bayes-nets explicitly encodes the `dependencies` between variables to model **joint distributions**. They are particularly useful because they provide a compact representation for practically arbitrary distributions, and efficient algorithms exist to sample and perform **inference over the joint distribution**.
 - It takes the idea of **uncertainty** and marry it with efficient structures. so..one can easily see what uncertain variable influence other uncertain variables.

## A2> Bayesian Network Reasoning Patterns  
<img src="https://user-images.githubusercontent.com/31917400/93623864-4cccda80-f9d7-11ea-8750-4784e84de874.jpg" />

### > Flow of influences...the `V-Structure` is interesting! 
<img src="https://user-images.githubusercontent.com/31917400/93917021-4fdf0800-fd02-11ea-9f23-c15fba2e0031.jpg" />
<img src="https://user-images.githubusercontent.com/31917400/93917802-5a4dd180-fd03-11ea-98d3-7dde2c68be67.jpg" />

### > Find the parameters...
 - ### (1) single result...(a single likelihood)
   <img src="https://user-images.githubusercontent.com/31917400/93803092-425f4a80-fc3c-11ea-80db-801a4466c645.jpg" />

 - ### (2) multiple results...(multiple likelihoods)
   <img src="https://user-images.githubusercontent.com/31917400/93878938-ca902f00-fcd2-11ea-8cba-4f12f7c9cac5.jpg" />

 - ### (3) between results ? **`P( likelihood_A | likelihood_B )`** <*><*><*><*><*> important!!!
   If we Know the **prior**, its **likelihoods** are independent because of the `conditional independence`... so? 
   - There goes magic!! If we see the prior is the **`hidden latent variable`**, then dealing with the features at hand becomes super simple since they are independent each other! 
   <img src="https://user-images.githubusercontent.com/31917400/93879530-c0226500-fcd3-11ea-8023-725535b46742.jpg" />

 - ### (4) multiple parameters..latent variables?...(multiple priors)
   This is also important. Using this V-Structure, we can make any features interlaced with each other!
   <img src="https://user-images.githubusercontent.com/31917400/93886109-eef10900-fcdc-11ea-8296-a25d93b7ad21.jpg" />

### > Typical Conditional Independence: the `SPLIT`
<img src="https://user-images.githubusercontent.com/31917400/93900089-e9032400-fcec-11ea-822a-a9d3fc39842f.jpg" />

### > D-Separation and V-Structure
 - D-Blocking in ordinary structures: The knowledge of any nodes on the influence stream will split the whole structure (the conditional independence gets activated).    
 - Activation in V-Structures: The knowledge of `"child"` renders previously independent variables **DEPENDENT** (the dependence gets activated). 
<img src="https://user-images.githubusercontent.com/31917400/67591895-6083a880-f756-11e9-992b-6bb649a348e4.jpg" />

> [Note] We don't have any obv. We can see the V-Structure, but its child is not observed.  D and S - are they really independent because of the inactivated child? A proof using marginalization...
   <img src="https://user-images.githubusercontent.com/31917400/94021208-abb19b80-fdab-11ea-9d43-048d667aeea0.jpg" />

> [Note] __Independence assumption in Naive Bayes Classification:__ Given the class variable, each observed variable is independent of the other observed variables. In other words, if we observe the class variable, influence cannot flow between any of the other child variables. It's like typical D-seperations. But Think! the Class has not yet been observed. So it's naive to say all features are independent? 
   <img src="https://user-images.githubusercontent.com/31917400/94045116-e96fed80-fdc6-11ea-9e62-14581ac9877b.jpg" />



## A3> Template Model (Dynamic Bayesian Network or Time Series Network)
 - Hidden Markov model (HMM)
 - Kalman filter (KFM)
 - Time series clustering, etc.
 
 This system evolves over time ? 
   - HMM: Although Hidden Markov Models can be viewed as a subclass of dynamic Bayesian networks, they have their own type of structure that makes them particularly useful for a broad range of applications.
   - 1) "Transition" Probability by time (b/w parents?)
   - 2) "Emission" Probability (for each child?)
   <img src="https://user-images.githubusercontent.com/31917400/94165291-f6054c00-fe81-11ea-8b09-9bb5ebe0b04f.jpg" />

__What is Template Model?__ As an extension on the language on graphical models, **Template Model** intends to deal with temporal processes where we have many replication over time. So..it extends standard Bayesian networks with the concept of time. They are a convenient way of representing Bayesian networks that have a high amount of parameter sharing and structure (however, they are merely compact representations of a fully unrolled Bayesian network, so it's not to say it has an additional representative powers).
 - **Template Variable:** it is the variables that we end up replicating in many cases **within a single model** as well as **across models**. The typical example is the locations (trajectories) of a robot given time period. ConditionalProbabilityDistribution in **template models** can often be copied many times.
 - **Template models** are just the dependency models from template variables.  
 - **Template models** can often capture events that occur in a **time series**. 
 - **Template models** can capture `parameter sharing` within a model.
 <img src="https://user-images.githubusercontent.com/31917400/52852977-071ca180-3112-11e9-8928-f44a07c0f347.jpg" />



## A4> Global / Local structure

> [Note] Model the repeatition! If we toss the same coin again and again, how to model this repeatition? Put a little box around that outcome variable, and this box which is called a plate(whyyy? coz it's a stack of identical pieces). A plate denotes that the outcome variable is **indexed**. Sometimes in many models, we will include all parameters explicitly within the model. But often when you have a parameter that's outside of all plates, we won't denote it explicitly. So we just omit it.
  <img src="https://user-images.githubusercontent.com/31917400/94169641-f48a5280-fe86-11ea-878d-7c235caf8a4b.jpg" />
   
> Plate dependency model has the following characteristics:
 - For a template variable `A{X1, X2,...,Xk}`indexed by `X` (ex. A: Intelligence, Xk: each student ID), 
 - For each of those template variables, we have a set of **template parents**. 
 - Each of the index in the template parents variable `B{U1, U2,..}`indexed by `U` or `C{V1, V2..}`indexed by `V`, etc have to be a subset of the index in the child.
 <img src="https://user-images.githubusercontent.com/31917400/94171074-b4c46a80-fe88-11ea-9695-779f91f1a9c7.jpg" />
   
 - From the ground network above, we can see that A and B belong only to plate x, C belongs to x and y, D belongs to x and z and E belongs to all 3. Moreover, there needs to be a direct edge from A to E. These models, by allowing us to represent an intricate network of dependencies, allow us to capture very richly correlated structures in a concise way which allows collective inference. These models can encode correlations across multiple objects allowing collective inference. 

## Local Structure ????
No more Tabular representations for CPD!!!!
 <img src="https://user-images.githubusercontent.com/31917400/94267607-cf9fe900-ff33-11ea-8536-34a59711d8b4.jpg" />

> Instead,...there are several local structures (in a parametric form) for **Conditional Probability Distributions**. And..we hope to reduce the parameter size, Using...1.Deterministic Structure?, 2.Tree Structure?, 3.Logistic Structure?, 4.Noisy(Or/And) Structure?, 5.Continuous Structure?
## `This is about the story of crazy V-Structures` 
... of Conditional Probability Distribution 

### a) Basic context-specific CPD
<> __Context-Specific Independent structure:__ The independent statement b/w two variable(X,Y) only holds for particular values of the conditioning variable c for example. So the dependence only happening in a certain context. 
<img src="https://user-images.githubusercontent.com/31917400/94425895-9b6f3700-0184-11eb-8faf-cd7caa52bf18.jpg" />


### b) Tree Structured CPD
<> __Context-Specific Independent tree:__ The independent statement b/w two variable(X,Y) only holds for particular values of the conditioning variable C for example. So the dependence is only happening in a certain context.
<img src="https://user-images.githubusercontent.com/31917400/94427673-5e587400-0187-11eb-9df4-7aafd946a1e4.jpg" />

<> __Non**-Context-Specific Independent tree (Multiplexer Model):__ As an additional structure, **multiplexer(as a Parent, a selector)** activates the `V-structure`. This will dramatically reduce the size of parameters.  
<img src="https://user-images.githubusercontent.com/31917400/94304746-f546e580-ff67-11ea-850b-030e2a7efa12.jpg" />

   - Application of the Multiplexer Tree
     - The Multiplexer Tree is very useful! It comes up in physical hardware configuration settings. It turns out that all of the troubleshooters that are part of the Microsoft operating system are, Built on top of a Bayesian Network Technology. The task is to try and figure out **why a printer isn't printing**. So we have a variable here that tells us whether the printer is producing output, and that depends on a variety of factors, but one of the factors that it depends on is where the printer input is coming from: `Is it coming from a local transport? Or a network transport?`. And, depending on which of those it's coming from, there's a different set of failures that might occur. So the variable here that serves the goal of the **selector(Multiplexer) variable** is this variable `print data out`. And that's the root of the tree that's used here. And and depending on whether the print location is local or not. then you depend either on properties of the local transport. Or on properties of the network transport. And it turns out that even in this very, very simple network, the use of tree CPD's `reduces the number of parameters` from 145 to about 55, and makes the elicitation process much easier. 
     <img src="https://user-images.githubusercontent.com/31917400/52902788-978bdc80-320d-11e9-935b-691a91a1e2a2.jpg" />


### c) Noisy(Or/And) Structured CPD
What if there are **so many factors** that contribute something to the probability of exhibiting phenomenon such as "cough"? 
<img src="https://user-images.githubusercontent.com/31917400/52904371-4e468780-3223-11e9-8c78-c72c7ab90c28.jpg" />

<> **Noisy-OR cpd** can capture such interaction. 
   - It is a larger graphical model where we break down the dependencies of Y on its parents (X1 up to Xk), by introducing a bunch of `intervening variables` as noisy transmitters or filters. So Y becomes true only if these filters succeeds in making it true. 
   - **Z** is a probability assignment machine. Even one single **Z** that turns out to be true, can activate **Y**... 
   - Then what is the probability that all of these **Z**guys fail to turn on the variable Y? So, when does `Y keeps sleeping`? First of all, when it doesn't get turned on by the **leak**(![formula](https://render.githubusercontent.com/render/math?math=\lambda_0)=**`P(Y get activated by itself)`**) . So, that's ![formula](https://render.githubusercontent.com/render/math?math=1-\lambda_0) x **`P(none of Z activate Y)`**.
   <img src="https://user-images.githubusercontent.com/31917400/94306201-6e473c80-ff6a-11ea-9091-a4432e1a2154.jpg" />
   
   - > **Therefore,... Given that Y = 0, we know that all ![formula](https://render.githubusercontent.com/render/math?math=\lambda_i) from ![formula](https://render.githubusercontent.com/render/math?math=Z_i) are 0; so that blocks the trail of influence from ![formula](https://render.githubusercontent.com/render/math?math=X_1toX_2)...so..all features are independent!
   
<> **Noisy-AND (Noisy_Max) cpd** can capture such interaction.
   - This is called independence of causal influence because it assumes that you have a bunch of causes and each of them acts independently to affect the truth of that child variable. so, there's no interactions between the different causes.
   - Each `Zi` have their own separate mechanism and ultimately it's all aggregated together in a single variable `Z` from which the truth of Y is then determined from this aggregate effect.  
   <img src="https://user-images.githubusercontent.com/31917400/94306496-f9c0cd80-ff6a-11ea-847a-7ee3590a29ea.jpg" />
   
   - > **Therefore,...Given that Y = 0, it's not to say all features are independent ???

### d) Logistic Structured CPD
<img src="https://user-images.githubusercontent.com/31917400/94437696-06753980-0196-11eb-8ab4-0169dbc9446f.jpg" />

 - In a sigmoid CPD, each discrete **Xi** induces a continuous `Zi` which represents `Wi*Xi` (convert `discrete` into `continuous`). 
 - `Wi` parameterizes this edge and tells us how much force **Xi** is going to exert on **making Y true** so, if `Wi` is zero, it tells us that **Xi** exerts no influence whatsoever. 
   - (+) `Wi`: **Xi** is going to make Y more likely to be true 
   - (-) `Wi`: **Xi** is going to make Y less likely to be true. 
 - the final `Z` adds up all of these different influences + **an additional bias term `W0`**. 
 - Then we turn this ultimately into the probability of the **target variable Y** by passing this continuous quantity `Z` through a Sigmoid Function(squelching func). 
   - Since **e to the power of `Z`** is a positive number, this gives us a number that is always in the interval of {0,1}.
   <img src="https://user-images.githubusercontent.com/31917400/94438687-5b657f80-0197-11eb-9218-4423552aac1d.jpg" />
   
 - > **Therefore, only the number of observed features bigger than certain threshold will activate Y !

### e) Continuous Structured CPD
<img src="https://user-images.githubusercontent.com/31917400/52906319-31b94800-3241-11e9-80b0-3e7b2fd646bf.jpg" />

 - When our network involves continuous variable..
   - Let's imagine that we have a continuous temperature variable and we have a sensor. Now thermometers aren't perfect, so what we would expect is that the sensor is around the right temperature but not quite. And so, one way to capture that is by saying that the sensor follows a normal distribution.
 <img src="https://user-images.githubusercontent.com/31917400/52906349-c7ed6e00-3241-11e9-8859-d0ac04e8257d.jpg" />


## A5> Decision Theory: 
Decision making under uncertainty

### a) Maximum Expected Utility
<img src="https://user-images.githubusercontent.com/31917400/94546911-6fb48580-0246-11eb-91d8-b067a983177c.jpg" />

 - Expected Utility: `E[U]`
   <img src="https://user-images.githubusercontent.com/31917400/94476796-da26e080-01c8-11eb-963a-c5e2038951c4.jpg" />

 - Maximum `E[U]` Decision Rule
   <img src=" " />


 - T.B.D
 
 
 


---------------------------------------------------------------------------------------------------------
# (B) Inference for Bays-Net
   <img src="https://user-images.githubusercontent.com/31917400/67621845-b1090d80-f80b-11e9-8081-dcd66dd9a27e.jpg" />
   
 - Q1. How to answer questions such as "Given some inputs, what are the outputs?" The answer is going to be a complete `joint` distribution over the **query variables**...we call it `posterior`. This is what we are after. 
 - Q2. Out of all the possible values for all the query variables, which combination of values has the highest probability? Whic `Q` values are maxable given the evidence values? 
 - Q3. One great thing about Bayes-net is that we are not restricted to going only in one direction; we can reverse the casual flow. The `Q` can become evidence values and the `E` can become the query values. Like wise, one `Q` and `E` can become evidence values and the other `Q` and `E` can become query values. The variable unspecified can become hidden variable. 
   - If Mary has called to report(it's true) that "Hey! the alarm is going off!!!"(don't know if it's true or not), we want to know if there has been a burglary. 
   <img src="https://user-images.githubusercontent.com/31917400/67622039-e0207e80-f80d-11e9-98c9-a121ac5855b4.jpg" />

?????????????????????????????????????????????????????????????????????????????????
-------------------------------------------------------------------------------------------------------------------------------------
> ## Let's see how to operationalize Bayes-Net to answer such **conditional probability** queries! 

The main issue is...
 - How to Compute **Marginals**?
 - How to Compute **MAP assignments**?
<img src="https://user-images.githubusercontent.com/31917400/94588251-993bd400-027b-11eb-890e-3698673d8c3f.jpg" />

 - <1> Using __Variable Elimination__ with Marginalization
 - <2> Using __Message passing over graph__ with MAP assignment (for special purpose?)
   - [Note] MAP Inference
     <img src="https://user-images.githubusercontent.com/31917400/95752402-e1a1bb80-0c97-11eb-8997-56f09080494e.jpg" /> It claims a single coherent assignment of highest probability, which is not the same as maximizing individual maginal probabilities.  
   - Max-product-Belief Propagation
   - ....
 - <3> Using __Random Sampling__ with Marginalization

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## > `Inference_01`: Enumeration and Variable Elimination  
Let's say...Go through all possibilities, add them up and come up with an answer. 
 - State the problem and ask the question: "If **Mary** and **John** has called to report that the alarm is going off, we want to know if there has been a **burglary**." 
 <img src="https://user-images.githubusercontent.com/31917400/67623036-735eb180-f818-11e9-9ad2-cbbcc6141961.jpg" />

 - First, take a conditional prob(posterior) and rewrite it as unconditional prob(a bunch of **`jointsss`**).
   <img src="https://user-images.githubusercontent.com/31917400/67623078-0992d780-f819-11e9-88b7-c4b0bae56255.jpg" />

 - Next, enumerate all the atomic probabilities and calculate the sum of products.
   - On the numerator, this joint can be determined by enumerating all hidden variable values..(Making the Sum over these hidden variables) 
     <img src="https://user-images.githubusercontent.com/31917400/67623248-dcdfbf80-f81a-11e9-87fe-b187545b1c73.jpg" />
 
   - To obtain the values of these atomic events, rewrite the eqation in a form that corresponds to the conditional prob-table of this Bayes-net. Rewrite w.r.t **parents** of each of the nodes in the network, so the form of the unfolded equation heavily depends on the graphic!  
     <img src="https://user-images.githubusercontent.com/31917400/67623317-8fb01d80-f81b-11e9-9653-07cc7f9cafdd.jpg" />
   
   - The equation can be understood as a function of hidden variables and the answer can be the **sum of all these function outputs** for all values of the hidden variables. So it's a sum of such terms and each of which is a product of "factors" in the previous equation.  
     <img src="https://user-images.githubusercontent.com/31917400/67623855-0cde9100-f822-11e9-8f82-bb14e7c04135.jpg" />

 - Do the same thing with the denominator. 
 - We finish to enumerate over all four hidden variable possibilities in the end, then it's saying `P(burglary alarm being true | John, Mary)` is 0.284.   

> ### To speed up, We can eliminate some variables...
 - ### Step 1> `Make a joint`
   <img src="https://user-images.githubusercontent.com/31917400/67634221-f59ab480-f8b0-11e9-8dc4-1e9a03ddbc90.jpg" />

 - ### Step 2> `Marginalize the joint`...keep making the "single node" until it gives an answer:
   <img src="https://user-images.githubusercontent.com/31917400/67634554-8e333380-f8b5-11e9-9007-af2d5aca5ce5.jpg" />

### Variable Elimination
pushing terms through the summation..
 - Find a Factor(joints) product -> Then...Marginalize
   <img src="https://user-images.githubusercontent.com/31917400/95770493-6220e600-0cb1-11eb-8eb8-a619f1cd0a31.jpg" />

 - Graph-based perspective
   : TBD

 - Elimination ordering? Which variable should be removed first?
   : TBD 

## > `Inference_02`: MAP
: TBD


## > `Inference_03`: Approximation Method by means of "Sampling"
To deal with `Joint` (or to estimate `Joint`), we actually do pseudo-experiments?

(+) Sampling has an advantage over inference 
 - In that we know a procedure for coming up with at least an approximate value for the `Joint`.  
 - In that although we don't have the **conditional probability tables**, we still can simulate the process.    
## "Sampling" means we can get a posterior at the end!
### `We can do sampling`: 
Draw samples then average them out. You have a machine dude!
<img src="https://user-images.githubusercontent.com/31917400/68958025-2e98bb80-07c3-11ea-9ebb-9503bedfb3c7.jpg" />

Let's say we have a bunch of inputs `X` that follows a **certain distribution**. We want to get **"Expected value of the outputs"** `E[f(X)]`, but how? using computer, we plug in all inputs then average out the outputs `f(X)`. If we know the input distribution, then we sample each input from the known distribution, then plug them in. But what if we have no knowledge on input distribution of `X`? 
 - What we can do is to think of some ulternative distribution! then draw samples from it. Interestingly, we can later on correct the samples from the alternative(wrong) distribution! And sometimes even we can do better than using the real distribution of `X` at the end of the day! HOW? 
 - ### 1) Importance Sampling... is not a sampling but a variant of MonteCarlo approximation method.
   - Let's say we have `E[f(x)] = ∫ f(x)*P(x) dx` where the pdf **P(x)** is the probability of **f(x) outcome**. 
   - we do some weird thing with `q(x)` that we call "proposal distribution". And it's ur baby. 
   <img src="https://user-images.githubusercontent.com/31917400/68993028-06fd2e00-086b-11ea-805d-775da9338e2a.jpg" />
   
     - Treat `f(x)*P(x) / q(x)` as a new objective function that we want to approximate. And **q(x)** is the **pdf** of our new objective function (so from now on, **`our samples come from q(x)`** and not from `P(x)`). And we can perform the MonteCarlo approximation on our new objective function! The result would be exactly what we seek for in the beginning. 
     <img src="https://user-images.githubusercontent.com/31917400/68996149-28bbdc80-088e-11ea-8869-07ca8b8c7b31.jpg" />
     
     - We know `f(x)` of course. But do we know `P(x)` where the sample `X` come from?? No! we cannot compute `P(x)`. We don't know the original samples to plug into `f(x)` for MonteCarlo Computation...perhaps..we do not know the exact `P(x)`, but sometimes we know sth similar to `P(x)`..but without the normalizing constant. 
       - Let's say
       <img src="https://user-images.githubusercontent.com/31917400/68995569-315ce480-0887-11ea-99cf-472009504fca.jpg" />
       
       - If we put them in..looks nice, but let's say we don't know the normalization constant `z_p`, `z_q`. 
       <img src="https://user-images.githubusercontent.com/31917400/68995679-438b5280-0888-11ea-9345-a6bdac11e7d1.jpg" />
       
       - So we don't know `z_p` and `z_q`, but luckily we can compute the proportion because we can approximate the **Normalization constant proportion** with the MonteCarlo approximation, using the "importance weight"!
       <img src="https://user-images.githubusercontent.com/31917400/68995820-eabcb980-0889-11ea-89e8-224c317db213.jpg" />
       
       - thus this is the MonteCarlo Estimation within the MonteCarlo Estimation.
       <img src="https://user-images.githubusercontent.com/31917400/68996074-0d040680-088d-11ea-8587-ffbf437c73f9.jpg" />

 - ### 2) Smirnov's Inverse Transform sampling 
   We have a `random variable`, and want to **generate samples** from the `random variable` or `pdf`, first, you need CDF!
   - a) When CDF of your data distribution is invertible: `inverse CDF(unif(0,1))` is your sample!
   <img src="https://user-images.githubusercontent.com/31917400/68999966-4ace5280-08c0-11ea-9600-9497a37949d4.jpg" />
   
   - b) When CDF of your data distribution is not invertible: playing with "intervals"..
   <img src="https://user-images.githubusercontent.com/31917400/69006832-eeede300-092c-11ea-8fb1-a12e13d7c021.jpg" />

 - ### 3) Rejection Sampling
   It also applies for a higher dimension. 
   - a) Draw samples using **Uniform distribution** on a "set A": `It's a discrete`!
     - The "set A" is very complicated. But we know a certain rectangle boundary that houses our "set A"
     - First, draw a bunch of samples from a larger set of a `certain known rectangle boundary`, then 
     <img src="https://user-images.githubusercontent.com/31917400/69007867-86f2c900-093b-11ea-9ad7-bea3631487c9.jpg" />
  
   - b) Draw samples using **Non-Uniform distribution** on a "pdf A": `It's a continuous`!
     - The "pdf A" is very complicated. If we don't know "pdf A", we can first think of the unnormalized verson(proportional to pdf A) like "pdf A_tilda". And we choose additionally the proposal distribution "q" for actual sampling(gives a boundary of uniform sampling). "pdf A_tilda" will work as a constraint to reject/accept the samples.       
     <img src="https://user-images.githubusercontent.com/31917400/69014553-53d42800-0983-11ea-8912-34609a85d966.jpg" />
  
 - ### 4) MCMC and Gibbs Sampling for multiple parameter inference
   Sampling can help a Neural Network model? 
<img src="https://user-images.githubusercontent.com/31917400/69341186-fb41ab00-0c60-11ea-8b34-17e8a851b5a6.jpg" /> 
   
   MarKov Chain 
   <img src="https://user-images.githubusercontent.com/31917400/69055084-e23cbe00-0a04-11ea-96f6-b56046fa7153.jpg" /> 
   <img src="https://user-images.githubusercontent.com/31917400/69059687-ea4d2b80-0a0d-11ea-9719-d43990924537.jpg" /> 

When `x ~ unknown P(x)`, we hypothetically sample from a proposal distribution `q(x)`(MonteCarlo) then approximate stationary distribution`E[P(x)]`(MarkovChain). In other words, instead of trying to deal with intractable computations involving the posterior, we can get samples from some easy distribution then feed these samples to our known joint function`g(x)`. Next, we use the proportion of the joint function outputs (`g(x1)`/`g(x0)` as Metropolis-Hastings ratio: α), or the random walk's transition probability distribution, we decide the final samples for the nasty `P(x)`.    
> Metropolis > Metropolis Hasting > Gibbs

When we have multiple parameters `P(θ,ϕ|y) ∝ g(θ,ϕ)`, first we plug in the value of arbitrary ϕ, pretending we know the value of θ by substituting in its current value or current iteration from the Markov chain. Once we've drawn for both θ and ϕ, that completes one iteration and we begin the next iteration by drawing a new θ. This idea of **one at a time updates** is used in what we call Gibbs sampling.
<img src="https://user-images.githubusercontent.com/31917400/69253066-e9ea9700-0bab-11ea-99ff-e4b73ed0cc48.jpg" /> 
<img src="https://user-images.githubusercontent.com/31917400/69254772-ac3b3d80-0bae-11ea-8bd3-e9e40b7f8625.jpg" /> 




---------------------------------------------------------------------------------------------------------
# (C) Learning Bayes-Net from data
<img src="https://user-images.githubusercontent.com/31917400/98442987-57b30a00-2100-11eb-8e59-c1379be346ab.jpg" />

## 00 > The Goal: Knowledge discovery
 - ### In Structure:
   - Check_1. directionality of edges ?
   - Check_2. independencies ?
   - Check_3. presence and location of hidden variables ?
   - Check_4. structure overfitting ?
     - How to penalize the structure complexity?....the more complex it is, the higher training-likelihood it will have
 - ### In Prediction on new instance:
   - Check_1. Estimated model parameter overfitting ?
     - it can overfit to random noise in training data
     - Use regularization....

### Why Bayes-Net for Knowledge discovery?
 - we can exploit correlations between several predicted variables.
 - In the decision analysis framework, traditional point estimation approaches have often produced faulty risk assessment results as it ignores the associated uncertainty. One can see that the key lies in the manifestation of uncertainty range (confidence interval) and this requires us to obtain a full parameter distribution. Bayesian method allows us to estimate a full parameter distribution, using the joint distribution of the assumed model parameters(prior) and the given observations(likelihood). 
 - Incorporate prior knowledge into our model..i.e...Bayesian method derives an insight based on the synthesis of the assumed knowledge in the parameters(prior) and the new information from the observed data(likelihood)...combining both observations and experts' knowledge on the most likely parameter values 
 - we can perform multiple tasks, using a single model. This can be a efficient framework of knowledge discovery

----------------------------------------------------------------------------------------------------
## 01 > Parameter Learning 
### Approach 01. MLE: 
`MLE` tries to estimate the best parameter while optimizing the likelihood of the data, given the parameters.
<img src="https://user-images.githubusercontent.com/31917400/99130277-c9f78300-2607-11eb-86d1-93deb97eab0f.jpg" />

T.B.D


### Approach 02. Bayesian Estimation
`MLE` is flawed...
> Limitations of **MLE**
 - [Case]: "Toss a coin and H came 7 times out of 10 tosses. Then P(H)=0.7" which is the `θ`.
   - New context:
     - **A** and **B** fight a duel. **A** won 7 out of 10 matches. Then P(A)=0.7 which is the `θ`.
   - Larger samples:
     - Toss a coin and H came 70,000 times out of 100,000 tosses. Then P(H)=0.7 which is the `θ`.
 - MLE has absolutely no ability to distinguish between these three scenarios above.  

> Bayesian Estimation in PGM offers some better properties. 
 - First, `θ` becomes a random variable. In Bayesian framework, **anything about we are uncertain** can be viewed as a **random variable** over which we have a distribution that is updated over time as data is obtained. This is the heart of the Bayesian formalism.  
   - In MLE, `θ` is fixed (or given), and all tosses(data points) are independent. 
   - In BE, `θ` is unknown, so we cannot assume all tosses are independent...they are marginally **dependent** because of their unknown mommy (without being given `θ`) 
   - This gives us a **joint probablistic model** (of all data points, and `θ`..evenly). 
   <img src="https://user-images.githubusercontent.com/31917400/99147104-f5b15200-2675-11eb-9686-a31f4c7e61d9.jpg" />

   - what about Bayesian prediction on new instances ?
     - For example, let's say we have a Multinomial Data distribution, thus it comes with a Dirichlet prior distribution.
     <img src="https://user-images.githubusercontent.com/31917400/99147890-4cba2580-267c-11eb-8c37-fa84c4440885.jpg" />

> Bayesian Estimation in Bayes-Net
 - Case 01.     
   <img src="https://user-images.githubusercontent.com/31917400/99149850-737e5900-2688-11eb-800b-d7af94bcfaec.jpg" />

 - Case 02.
   <img src="https://user-images.githubusercontent.com/31917400/99150158-81cd7480-268a-11eb-8338-8344f720a1e9.jpg" />

In Bayes-Net, if the model has independent priors, then its posteriors are also independent.

----------------------------------------------------------------------------------------------------
## 02 > Structure Learning (Model Selection?)
 - Case_01: Answering specific queries by taking data and learning the most significant dependencies...but we don't know the structure.
 - Case_02: Discovering the interrelationships between the variables so that we understand the our whole network better...but we don't know the structure.
 - What's the Problem?
   <img src="https://user-images.githubusercontent.com/31917400/99152105-aaa83680-2697-11eb-82d8-3f07bb782913.jpg" />

 - Solution: **Scroing based Learning** (Optimization?)
   - We can define a scoring function that evaluates how well the network structure matches your data. 
   <img src="https://user-images.githubusercontent.com/31917400/99152228-5d789480-2698-11eb-8694-e7d1a69547df.jpg" />

### Scoring Criteria
 - 1. Likelihood Score
   - Find the (model, `θ`) pair that maximize the likelihood?
     - It computes the log-likelihood of data relative to a certain structure, using MLE parameters(already optimized) for the structure.   
     - `It is subject to overfitting problem for sure...`
     - which structure shows bigger score?
       <img src="https://user-images.githubusercontent.com/31917400/99153519-ef849b00-26a0-11eb-9194-53c4b0359ef7.jpg" />
 - 2. BIC, Asymptotic Consistency
 
 - 3. Bayesian Score


### Searching Structures with Optimization (**Exploit Decomposability**)
> Input: 
  - your data
  - scoring criteria selection
  - prior information
  - a set of possible structures
> Output: 
  - a structure that maximizes the score





----------------------------------------------------------------------------------------------------
## 03 > Learning with incomplete data
What's the occasion?
 - hidden variables? Unobservable?
 - simply missing values?

The presence of missing values or latent variable raises multiple challenges.
 - (1) Unknown mechanism of missingness
 - (2) Complexity of likelihood & Multiple Global Optima

## (1) Unknown mechanism of missingness

### With Latent variables and Model Sparcity
Having a latent variable sometimes gives an advantage.
 - Latent variable often gives rise to the **sparser** and therefore **easier-to-learn** models. 
 - Latent variable often offers an interesting characterization of structure in the data...such as clusters..
   <img src="https://user-images.githubusercontent.com/31917400/99156871-73984c00-26bc-11eb-86ca-95836423af47.jpg" />

### With missing values
Having missing values gives a pain in the ass. H,T,H,?,T,?,?,?,T,H......how to deal with "?" If you don't know why these data are missing, you have no idea how to proceed... 
 - __Missing data mechanism:__
   <img src="https://user-images.githubusercontent.com/31917400/99159390-b6b1e980-26d3-11eb-9c0e-72c0e0bb714a.jpg" />

   - **[Case 01]** with Random missing value
     <img src="https://user-images.githubusercontent.com/31917400/99159551-2e344880-26d5-11eb-89c3-c30fb9796617.jpg" />
     - The observed target value `Y` depends on `X` and on `O`, but there is no interaction between `X` and on `O` (D-Separation) 

   - **[Case 02]** with Non-Random missing value
     <img src="https://user-images.githubusercontent.com/31917400/99159697-cd0d7480-26d6-11eb-8f03-4d2cd533c72e.jpg" />
     - By comparison, in this case, the true value of the `X` variable affects `O`(observed or not)

 - __In the case of **missing at random** (MAR) we can ignore the `missing data mechanism` and focus only on the **likelihood that we get to observe**.__ 
   - The joint over (x, y, o) have the following characteristics that the observation variables `O` are independent of the missing `X`'s. This means if you tell me the `Y` values that you observe, then the fact that some `X` values may or may not have been observed doesn't carry any additional information. 
     <img src="https://user-images.githubusercontent.com/31917400/99183382-315e2180-2733-11eb-9268-4f2b9a757b94.jpg" /> 


## (2) Complexity of likelihood & Multiple Global Optima
 - Let's say if our `hidden variable` has two possible outcomes, then our `likelihood function` can have two global maxima. With many hidden variables, there can be an exponential number of global maxima. This can occur with missing data (not only hidden variables) as well.   
   <img src="https://user-images.githubusercontent.com/31917400/99187988-a6405400-2751-11eb-8c5b-b051ba20a6e9.jpg" /> 

 - parameters start being correlated with each other....
   <img src="https://user-images.githubusercontent.com/31917400/99188233-cc1a2880-2752-11eb-88e4-aa1df18e6512.jpg" /> 


> # Ok, then how to go about doing parameter estimation in the context of the missing data?

----------------------------------------------------------------------------------------------------------------------------------
## EM Algorithm (Likelihood Optimization)
In the context of missing data, the likelihood function looks like a nasty, complicated multi-modal function, which is impossible to optimize in closed form. There is two general classes of strategies. 
- The first is to use a generic optimization method, such as `gradient ascent`. We might start out with a particular point in the parameter space, and we compute the gradient at that point, and we go in the direction of steepest ascent, which might take us to the next point, at which point we compute the gradient, and we continue until we reach a local optimum of the function that we're trying to optimize. 
  <img src="https://user-images.githubusercontent.com/31917400/99191475-d34a3200-2764-11eb-8d1f-c8e778647de7.jpg" /> 
  
  - For improving the rate of convergence of these algorithms, some methods such as **line search** or **conjugate gradient methods** basically are going to get us faster to whatever local optimum we're going to end up at..
  - Need to run inference over each data instance at every iteration..so very costly...

- The second strategy is `EM-Algorithm` and that is specifically geared for likelihood function optimization. So it's a special purpose algorithm. The intuition is that if we had the full set of parameters, then computing the probability of the missing data would also be easy in the sense that it can be done using straight probabilistic inference. We have two sets of of things that we need to infer or estimate. One is the parameters, and the other is the missing data. We start out with one set of parameters, use that to estimate the values of the missing data and then use that completion to re-estimate the parameters and so on and so forth until we reach convergence.
  - First, pick a starting point for parameter value.
  - Next iterate:
    - [Step_E]: "complete" the data(soft completion using probability), using current parameters.
    - [Step_M]: Re-estimate the parameters relative to the previous data completion.
      <img src="https://user-images.githubusercontent.com/31917400/99192093-e232e380-2768-11eb-95bb-e85be1e0069c.jpg" /> 
      <img src="https://user-images.githubusercontent.com/31917400/99192675-fe844f80-276b-11eb-9046-173a8635e1ad.jpg" /> 

 - The convergence of the likelihood function is not the same as convergence of the parameters and so we have to decide which one we actually care about.
 - EM achieves only a **local optimum** of the log likelihood function. `Local optima are unavoidable, and increase with the amount of missing data.....`  They decrease with the total amount of data, but not if we hidden variables, at which point you're stuck with them no matter how much data you have.
 - Perhaps the most common use of the EM algorithm is to the problem of Learning with Latent Variables. These are situations where there is a certain set of variables that we just never get to observe, but they turn out to be important for capturing some important latent structure in the distribution of the data instances that we have. Perhaps the simplest example is in context of clustering where we have some kind of, latent class variable and some set of observed features. And we're trying to, basically segment the instances that we have into categories where, we assume that, for each category there is a similar distribution over the observed features. The features become independent to each other, once we're given the class. Latent variables satisfy MAR, so can use EM. 
















