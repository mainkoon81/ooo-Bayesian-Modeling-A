# ooo-Minkun-Model-Collection-VI-Bayesian-C

## Probabilistic Graphical Model
<img src="https://user-images.githubusercontent.com/31917400/52655869-1a025c80-2eed-11e9-82ba-1fdea931596f.jpg" />

It's a probabilistic model for which a graph expresses the **conditional dependence structure** between random variables.
 - Let's say we want to classify data points that are independent of each other(for example, given an image, predict whether it contains a cat or a dog), but See `I`, `like`, `machine`, `learning`... Problem here is that `learning` could be a noun or a verb depending on its context. Probabilistic graphical model is a powerful framework which can be used to learn such models with **dependency**.
 - PGM consists of a graph structure. Each `node` of the graph is associated with a **random variable**, and the `edge` in the graph are used to encode **relations** between the random variables. Because of the way the graph structure encodes the `parameterization` of the probability distribution,
   - It gives us an intuitive and compact data structure for capturing **high dimensional probability distributions**. 
   - It gives us a suite of methods for **efficient reasoning**, using general purpose algorithms.
   - It gives us a reduction in the number of parameters thus we can represent these high-dimensional probability distribution efficiently using a very small number of parameters. 
     - By hand: feasible elicitation
     - Automatically: learning from data
   
Depending on whether the graph is **directed or undirected**, we can classify graphical modes into two categories.
 - Bayesian networks
 - Markov networks
<img src="https://user-images.githubusercontent.com/31917400/52657674-18d32e80-2ef1-11e9-8102-e5b5977b0752.jpg" />

# A. Representation
### 1> Bayesian Network
<img src="https://user-images.githubusercontent.com/31917400/52790734-36bea180-305f-11e9-83b4-d831b3ac13eb.png" />

It uses a `directed graph` as the intrinsic representation. Bayesian Network is a Directed Acyclic Graph(DAG) whose nodes represent the random variables X1, X2, ... It represents a `joint distribution`(via the chainRule) for Bayesian Networks.  

Bayes-nets explicitly `encodes the dependencies` between variables to **model joint distributions**. They are particularly useful because they provide a compact representation for **practically arbitrary distributions**, and efficient algorithms exist to sample and perform inference over the joint distribution.
 - It takes the idea of **uncertainty** and marry it with efficient structures.
 - one can easily see what uncertain variable influence other uncertain variables.
 
 - ### A single result
<img src="https://user-images.githubusercontent.com/31917400/67561343-8a1be000-f714-11e9-9583-74bcd84a13ad.jpg" />

 - ### What if we have multiple test results? `result01`, `result02`, ...
<img src="https://user-images.githubusercontent.com/31917400/67567229-6ca14300-f721-11e9-95f0-7493cd287be1.jpg" />

 - ### between result ? **`P( result02 | result01 )`**
<img src="https://user-images.githubusercontent.com/31917400/67569336-7aa59280-f726-11e9-8a70-2e7ed57ed008.jpg" />

 - ### What if we have multiple latent variables(hidden causes)? 
<img src="https://user-images.githubusercontent.com/31917400/67586119-c5d09d00-f748-11e9-894d-4e9f5f37de97.jpg" />

### Why Bayes-nets?
It defines probability distributions over **graphs of random variables**. Instead of enumerating all possibilities of combinations of multiple random variables, it defines probability distributions that are inherent to each individual node. The definition of this joint distribution bu using such factors has one great advantage: `we can reduce the number of probability values(parameters) required`.
<img src="https://user-images.githubusercontent.com/31917400/67589802-3ed3f280-f751-11e9-8de9-a5eca09adb8b.jpg" />

### D-Separation
The knowledge of "child" renders previously independent variables DEPENDENT!
<img src="https://user-images.githubusercontent.com/31917400/67591895-6083a880-f756-11e9-992b-6bb649a348e4.jpg" />


### [Template Model]:
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

## Global Structure
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

## Local Structure
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

### 2> Markov Network

It uses a `undirected graph` as the intrinsic representation. 


## Global Structure


## Local Structure





---------------------------------------------------------------------------------------------------------
# B. Inference
<img src="https://user-images.githubusercontent.com/31917400/67621845-b1090d80-f80b-11e9-8081-dcd66dd9a27e.jpg" />

 - Q1. How to answer questions such as "Given some inputs, what are the outputs?" The answer is going to be a complete `joint` distribution over the **query variables**...we call it `posterior`. This is what we are after. 
 - Q2. Out of all the possible values for all the query variables, which combination of values has the highest probability? Whic `Q` values are maxable given the evidence values? 
 - Q3. One great thing about Bayes-net is that we are not restricted to going only in one direction; we can reverse the casual flow. The `Q` can become evidence values and the `E` can become the query values. Like wise, one `Q` and `E` can become evidence values and the other `Q` and `E` can become query values. The variable unspecified can become hidden variable. 
   - If Mary has called to report that the alarm is going off, we want to know if there has been a burglary. 
   <img src="https://user-images.githubusercontent.com/31917400/67622039-e0207e80-f80d-11e9-98c9-a121ac5855b4.jpg" />

### Inference_01: Enumeration Method
Go through all possibilities, add them up and come up with an answer. 
 - State the problem and ask the question: "If **Mary** and **John** has called to report that the alarm is going off, we want to know if there has been a **burglary**." 
 <img src="https://user-images.githubusercontent.com/31917400/67623036-735eb180-f818-11e9-9ad2-cbbcc6141961.jpg" />

 - First, take a conditional prob and rewrite it as unconditional prob(using bayes rule).
 <img src="https://user-images.githubusercontent.com/31917400/67623078-0992d780-f819-11e9-88b7-c4b0bae56255.jpg" />

 - Next, enumerate all the atomic probabilities and calculate the sum of products.
   - On the numerator, this joint can be determined by enumerating all hidden variable values..(Making the Sum over these hidden variables) 
   <img src="https://user-images.githubusercontent.com/31917400/67623248-dcdfbf80-f81a-11e9-87fe-b187545b1c73.jpg" />
 
   - To obtain the values of these atomic events, rewrite the eqation in a form that corresponds to the conditional prob-table of this Bayes-net. Rewrite w.r.t **parents** of each of the nodes in the network.  
   <img src="https://user-images.githubusercontent.com/31917400/67623317-8fb01d80-f81b-11e9-9653-07cc7f9cafdd.jpg" />
   
   - The equation can be understood as a function of hidden variables and the answer can be the **sum of all these function outputs** for all values of the hidden variables. So it's a sum of such terms and each of which is a product of "factors" in the previous equation.  
   <img src="https://user-images.githubusercontent.com/31917400/67623855-0cde9100-f822-11e9-8f82-bb14e7c04135.jpg" />

 - Do the same thing with the denominator. 
 - We finish to enumerate over all four hidden variable possibilities in the end, then it's saying `P(burglary alarm being true | John, Mary)` is 0.284.   

We can speed up the enumeration. 















---------------------------------------------------------------------------------------------------------
# C. Learning






