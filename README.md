# What is PGM ?
: It's a probabilistic model for which a graph expresses the **conditional dependence structure** between random variables.

: Understanding what makes **`Conditional Independence`** b/w variables helps us explain some uncertainty reasoning.

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
## 1> Bayesian Network Intro
<img src="https://user-images.githubusercontent.com/31917400/93762637-e11d8400-fc07-11ea-936a-af4382c997bf.jpg" />

It uses a `directed graph` as the intrinsic representation. Bayesian Network is a Directed Acyclic Graph(DAG) whose nodes represent the random variables X1, X2, ... It represents a `joint distribution`(via the chainRule) for Bayesian Networks. Bayes-nets explicitly encodes the `dependencies` between variables to model **joint distributions**. They are particularly useful because they provide a compact representation for practically arbitrary distributions, and efficient algorithms exist to sample and perform **inference over the joint distribution**.
 - It takes the idea of **uncertainty** and marry it with efficient structures. so..one can easily see what uncertain variable influence other uncertain variables.

### Reasoning Patterns  
<img src="https://user-images.githubusercontent.com/31917400/93623864-4cccda80-f9d7-11ea-8750-4784e84de874.jpg" />

### Flow of influences...the `V-Structure` is interesting! 
<img src="https://user-images.githubusercontent.com/31917400/93917021-4fdf0800-fd02-11ea-9f23-c15fba2e0031.jpg" />
<img src="https://user-images.githubusercontent.com/31917400/93917802-5a4dd180-fd03-11ea-98d3-7dde2c68be67.jpg" />

### Find the parameters...
 - ### (1) single result...(a single likelihood)
   <img src="https://user-images.githubusercontent.com/31917400/93803092-425f4a80-fc3c-11ea-80db-801a4466c645.jpg" />

 - ### (2) multiple results...(multiple likelihoods)
   <img src="https://user-images.githubusercontent.com/31917400/93878938-ca902f00-fcd2-11ea-8cba-4f12f7c9cac5.jpg" />

 - ### (3) between results ? **`P( likelihood_A | likelihood_B )`**
   If we Know the **prior**, its **likelihoods** are independent because of the `conditional independence`... so? 
   <img src="https://user-images.githubusercontent.com/31917400/93879530-c0226500-fcd3-11ea-8023-725535b46742.jpg" />

 - ### (4) multiple parameters..latent variables?...(multiple priors)
   <img src="https://user-images.githubusercontent.com/31917400/93886109-eef10900-fcdc-11ea-8296-a25d93b7ad21.jpg" />

### Typical Conditional Independence
<img src="https://user-images.githubusercontent.com/31917400/93900089-e9032400-fcec-11ea-822a-a9d3fc39842f.jpg" />

### D-Separation and V-Structure
 - Activation: The knowledge of `"child"` renders previously independent variables **DEPENDENT**!
<img src="https://user-images.githubusercontent.com/31917400/67591895-6083a880-f756-11e9-992b-6bb649a348e4.jpg" />

### > Why Bayes-nets?
It defines probability distributions over **graphs of random variables**. Instead of enumerating all possibilities of combinations of multiple random variables, it defines probability distributions that are inherent to each individual node. The definition of this joint distribution bu using such factors has one great advantage: `we can reduce the number of probability values(parameters) required`.
<img src="https://user-images.githubusercontent.com/31917400/67589802-3ed3f280-f751-11e9-8de9-a5eca09adb8b.jpg" />


### What is Template Model?
As an extension on the language on graphical models, **TemplateModel** intends to deal with the very large class of cases. 
 - Template Variable: it is the variables that we end up replicating in many cases again and again within a single model as well as across models. Template model is the dependency models from template variables.  
 - **Template models** can often capture events that occur in a time series. 
 - **Template models** can capture `parameter sharing` within a model.
 - ConditionalProbabilityDistribution in **template models** can often be copied many times.
   - They are a convenient way of representing Bayesian networks that have a high amount of parameter sharing and structure. At the end of the day, however, they are merely compact representations of a fully unrolled Bayesian network, and thus have no additional representative powers.
<img src="https://user-images.githubusercontent.com/31917400/52852977-071ca180-3112-11e9-8928-f44a07c0f347.jpg" />

For example,
 - Dynamic Bayesian Network(DBN): to deal with temporal processes where we have replication over time.
 - Object Relational Model:
   - Directed: Bayesian Network
   - Undirected: Markov Network

How do you represent the dependency model over that ensemble in a coherent way?

### Global Structure
> Temporal Model(DBN) with TimeSeries:
 - Template Model incorporates multiple copies of the same variable thus allows us to represent multiple models within a single representation.
 - Plus, this system evolves over time - Dynamic Bayesian Network
 
> Temporal Model(HMM):
 - Although Hidden Markov Models can be viewed as a subclass of dynamic Bayesian networks, they have their own type of structure that makes them particularly useful for a broad range of applications.

> Plate Model:
 - Model the repeatition! If we toss the same coin again and again, how to model this repeatition? 
   - put a little box around that outcome variable, and this box which is called a plate(whyyy? coz it's a stack of identical pieces). A plate denotes that the outcome variable is **indexed**. 
   - sometimes in many models, we will include all parameters explicitly within the model. But often when you have a parameter that's outside of all plates, we won't denote it explicitly. So we just omit it.
<img src="https://user-images.githubusercontent.com/31917400/52870574-11ee2b00-3140-11e9-9ac1-a8ce07c4bb91.jpg" />
   
   - In sum, Plate dependency model has the following characteristics:
     - For a template variable `A{X1, X2,...,Xk}`indexed by `X` (ex. A: Intelligence, Xk: each student ID), 
     - For each of those template variables, we have a set of **template parents**. 
     - Each of the index in the template parents variable `B{U1, U2,..}`indexed by `U` or `C{V1, V2..}`indexed by `V`, etc have to be a subset of the index in the child.
   - __Ground Network__
   <img src="https://user-images.githubusercontent.com/31917400/52872945-aad37500-3145-11e9-87b8-838e19aeed7b.jpg" />
   
   - From the ground network above, we can see that A and B belong only to plate x, C belongs to x and y, D belongs to x and z and E belongs to all 3. Moreover, there needs to be a direct edge from A to E.
   - These models, by allowing us to represent an intricate network of dependencies, allow us to capture very richly correlated structures in a concise way which allows collective inference. These models can encode correlations across multiple objects allowing collective inference. 

### Local Structure
<img src="https://user-images.githubusercontent.com/31917400/52900377-03aa1880-31ed-11e9-8100-4386992ee220.jpg" />

There are several structures in a parametric form within Conditional Probability Distribution. We hope to reduce the parameter size...but HOW? 
 - a)Deterministic Structure
 - b)Tree Structure
 - c)Logistic Structure
 - d)Noisy(Or/And) Structure
 - e)Continuous Structure

> a) Deterministic Structure
<img src="https://user-images.githubusercontent.com/31917400/52900959-f98c1800-31f4-11e9-8daa-67710a994fa0.jpg" />

 - Context-Specific Independent structure
   - The independent statement b/w two variable(X,Y) only holds for particular values of the **conditioning variable C**. So the dependence only happening in a certain context. 

> b) Tree Structure
<img src="https://user-images.githubusercontent.com/31917400/52902425-6c52be80-3208-11e9-8f57-130d90e55ef1.jpg" />

 - Context-Specific Independent tree
   - The independent statement b/w two variable(X,Y) only holds for particular values of the **conditioning variable C**. So the dependence is only happening in a certain context.
 - **Non**-Context-Specific Independent tree (Multiplexer Model)
   - As an additional structure, **Multiplexer(as a Parent)** activates the `V-structure`. This will dramatically reduce the size of parameters.  
<img src="https://user-images.githubusercontent.com/31917400/52902687-1c75f680-320c-11e9-9b0d-ca8af4f6ca8f.jpg" />

   - Application of the Multiplexer Tree
     - The Multiplexer Tree is very useful! It comes up in physical hardware configuration settings. It turns out that all of the troubleshooters that are part of the Microsoft operating system are, Built on top of a Bayesian Network Technology. The task is to try and figure out **why a printer isn't printing**. So we have a variable here that tells us whether the printer is producing output, and that depends on a variety of factors, but one of the factors that it depends on is where the printer input is coming from: `Is it coming from a local transport? Or a network transport?`. And, depending on which of those it's coming from, there's a different set of failures that might occur. So the variable here that serves the goal of the **selector(Multiplexer) variable** is this variable `print data out`. And that's the root of the tree that's used here. And and depending on whether the print location is local or not. then you depend either on properties of the local transport. Or on properties of the network transport. And it turns out that even in this very, very simple network, the use of tree CPD's `reduces the number of parameters` from 145 to about 55, and makes the elicitation process much easier. 
     <img src="https://user-images.githubusercontent.com/31917400/52902788-978bdc80-320d-11e9-935b-691a91a1e2a2.jpg" />

> c) Noisy(Or/And) Structure
<img src="https://user-images.githubusercontent.com/31917400/52904371-4e468780-3223-11e9-8c78-c72c7ab90c28.jpg" />

 - What if there are **so many factors** that contribute something to the probability of exhibiting phenomenon? 
 - **Noisy-OR model** can capture such interaction. 
   - It is a larger graphical model where we break down the dependencies of Y on its parents (X1 up to Xk), by introducing a bunch of `intervening variables`. They are noisy transmitters or filters. So Y becomes true only if these filters succeeds in making it true. 
   - Then what is the probability that all of these **Z**guys fail to turn on the variable Y? So, when does y fail to get turned on?
     - First of all, when it doesn't get turned on by the `leak`. So, that's one minus lambda zero x the probability that none of Z causes Y turned on.
   <img src="https://user-images.githubusercontent.com/31917400/52904648-b9de2400-3226-11e9-8a9d-7dee3fabeaa2.jpg" />
   
 - **Noisy-AND(Noisy_Max) model** can capture such interaction.
   - This is called independence of causal influence because it assumes that you have a bunch of causes and each of them acts independently to affect the truth of that child variable. so, there's no interactions between the different causes.
   - Each `Zi` have their own separate mechanism and ultimately it's all aggregated together in a single variable `Z` from which the truth of Y is then determined from this aggregate effect.  
   <img src="https://user-images.githubusercontent.com/31917400/52904801-f874de00-3228-11e9-99cc-56067beca889.jpg" />

> d) Logistic Structure
<img src="https://user-images.githubusercontent.com/31917400/52904828-6e794500-3229-11e9-9e37-aca824bc0268.jpg" />

 - In a sigmoid CPD, each discrete **Xi** induces a continuous `Zi` which represents `Wi*Xi`. 
 - `Wi` parameterizes this edge and tells us how much force **Xi** is going to exert on **making Y true** so, if `Wi` is zero, it tells us that **Xi** exerts no influence whatsoever. 
   - (+) `Wi`: **Xi** is going to make Y more likely to be true 
   - (-) `Wi`: **Xi** is going to make Y less likely to be true. 
 - the final `Z` adds up all of these different influences + **an additional bias term `W0`**. 
 - Then we turn this ultimately into the probability of the **target variable Y** by passing this continuous quantity `Z` through a Sigmoid Function(squelching func). 
   - Since **e to the power of `Z`** is a positive number, this gives us a number that is always in the interval of {0,1}.

> e) Continuous Structure
<img src="https://user-images.githubusercontent.com/31917400/52906319-31b94800-3241-11e9-80b0-3e7b2fd646bf.jpg" />

 - When our network involves continuous variable..
   - Let's imagine that we have a continuous temperature variable and we have a sensor. Now thermometers aren't perfect, so what we would expect is that the sensor is around the right temperature but not quite. And so, one way to capture that is by saying that the sensor follows a normal distribution.
 <img src="https://user-images.githubusercontent.com/31917400/52906349-c7ed6e00-3241-11e9-8859-d0ac04e8257d.jpg" />









---------------------------------------------------------------------------------------------------------
# (B) Inference
<img src="https://user-images.githubusercontent.com/31917400/67621845-b1090d80-f80b-11e9-8081-dcd66dd9a27e.jpg" />

 - Q1. How to answer questions such as "Given some inputs, what are the outputs?" The answer is going to be a complete `joint` distribution over the **query variables**...we call it `posterior`. This is what we are after. 
 - Q2. Out of all the possible values for all the query variables, which combination of values has the highest probability? Whic `Q` values are maxable given the evidence values? 
 - Q3. One great thing about Bayes-net is that we are not restricted to going only in one direction; we can reverse the casual flow. The `Q` can become evidence values and the `E` can become the query values. Like wise, one `Q` and `E` can become evidence values and the other `Q` and `E` can become query values. The variable unspecified can become hidden variable. 
   - If Mary has called to report(it's true) that "Hey! the alarm is going off!!!"(don't know if it's true or not), we want to know if there has been a burglary. 
   <img src="https://user-images.githubusercontent.com/31917400/67622039-e0207e80-f80d-11e9-98c9-a121ac5855b4.jpg" />

## > Inference_01: Enumeration Method
Go through all possibilities, add them up and come up with an answer. 
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
 - `Make a joint`:
 <img src="https://user-images.githubusercontent.com/31917400/67634221-f59ab480-f8b0-11e9-8dc4-1e9a03ddbc90.jpg" />

 - `Marginalize the joint` then make a joint, marginalize the joint...keep making the "single node" until it gives an answer:
 <img src="https://user-images.githubusercontent.com/31917400/67634554-8e333380-f8b5-11e9-9007-af2d5aca5ce5.jpg" />

## > Inference_02: Approximation Method by means of "Sampling"
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

----------------------------------------------------------------------------------------
## Bayesian Neural Network
<img src="https://user-images.githubusercontent.com/31917400/69341233-14e2f280-0c61-11ea-80ef-26159e0fd58b.jpg" /> 10 years ago, people used to think that Bayesian methods are mostly suited for small datasets because it's computationally expensive. In the era of Big data, our Bayesian methods met deep learning, and people started to make some mixture models that has neural networks inside of a probabilistic model.

NN performs a given task by learning on examples without having prior knowledge about the task. This is done by finding an optimal point estimate for the weights in every node. Generally, the NN **using point estimates as weights** perform well with large datasets, but they fail to express uncertainty in regions with little or no data, leading to overconfident decisions. 

BNNs are comprised of a Probabilistic Model and a Neural Network. The intent of such a design is to combine the strengths of Neural Networks and Stochastic modeling. NN exhibits **universal continuous function approximator** capabilities. Bayesian Stochastic models generate a complete posterior(constructing the distribution of the parameters) and produce **probabilistic guarantees on the predictions**.  
 - In BNNs usually, a `prior` is used to describe the key parameters, which are then utilized as input to a neural network. The neural networks’ output is utilized to compute the `likelihood`. From this, one computes the `posterior` of the parameters by **Sampling** or **Variational Inference**. 
 - But BNNs are computationally expensive, because of the sampling or variational inference steps. BNNs have been demonstrated to be competent on moderately sized datasets and not yet fully explored with vastly large datasets. 

> WHY BNN?
 - Complexity is in the context of deep learning best understood as complex systems. Systems are ensembles of agents which interact in one way or another. These agents form together a whole. One of the fundamental characteristics of complex systems is that these agents potentially interact non-linearly. There are two disparate levels of complexity: 
   - simple or restricted complexity
   - complex or general complexity
 - While general complexity can, by definition, not be mathematically modelled in any way, restricted complexity can. Given that mathematical descriptions of anything more or less complex are merely models and not fundamental truths, we can directly deduce that Bayesian inference is more appropriate to use than frequentist inference. Systems can change over time, regardless of anything that happened in the past, and can develop new phenomena which have not been present to-date. This point of argumentation is again very much aligned with the definition of complexity from a social sciences angle. In Bayesian inference, we do learn the model parameters θ in form of probability distributions. Doing so, we keep them flexible and can update their shape whenever new observations of a system arrive.
 - So far, there has no deterministic mathematical formalism been developed for non-linear systems and will also never be developed, because complex systems are, by definition, non-deterministic. In other words, if we repeat an experiment in a complex system, the outcome of the second experiment won’t be the same as of the first. If so.. what is the obvious path to go whenever we cannot have a deterministic solution for anything? we approximate!!! This is precisely what we do in Bayesian methods: the intractable posterior `P(θ|D)` is approximated, either by a **variational distribution `g(θ|D)`** in neural networks, or with **Monte Carlo methods `q(θ|D)`**(envelop) in probabilistic graphical models.
 - Any deep learning model is actually a complex system by itself. We have `neurons`(agents), and `non-linear activation functions` between them(agents’ non-linear relations).
## Neural Networks are one of the few methods which can find `non-linear relations` between random variables. 

> How to BNN?
Problem: Big data?
<img src="https://user-images.githubusercontent.com/31917400/69342568-bb2ff780-0c63-11ea-9287-69eccb0dbc83.jpg" /> 

### Langevin MonteCarlo can save us?
<img src="https://user-images.githubusercontent.com/31917400/69347963-49f54200-0c6d-11ea-97eb-62eb7defcbd2.jpg" /> 



> some potential downsides in using Gibbs sampling for approximate inference in Bayesian Neural Networks
 - The Gibbs sampler generates one coordinate of the weight vector `w` at a time, which may be very slow for neural networks with tens of millions of weights.
 - The Gibbs sampler may not work with minibatching, i.e. we will have to look through the whole dataset to perform each step of the sampler. Thus, training on large datasets will be very slow.
 - [note] We will have to wait until the Gibbs sampler converges and starts to produce samples from the correct distribution, but this only needs to be done on the training stage. On the test stage, we will use the weight samples collected during the training stage to predict the label for a new test object, so predicting the labels for new test samples will not be necessarily slow.

## Dynamic Bayesian Neural Network


 













