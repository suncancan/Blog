# Coupled Matrix Factorization within Non-IID Context #

**Time:2015**

**Conference:PAKDD**

**Author:Fangfang Li, Guandong Xu, and Longbing Cao**

## Introduction ##
The existing **similarity methods** such as **Pearson** or **Jaccard** measures can be applied to compute the similarities within users or items, based on the **IID** assumption. 

In reality, however this assumption is not always held and there are more or less exist **coupling relations** between instances and attributes. One observation is that **the similarity of two attributes values** are dependent on other **attributes**, for example, two directors’ relationship is dependent on “Actor” and “Genre” attributes over all the movies. This dependent relation is called the **intercoupled similarity** between attributes. Alternatively, within an attribute, **one attribute value** will also be dependent on **other values of the same attribute**. Specifically, two attribute values are similar if they present the **analogous frequency distribution** on one attribute, which leads to another so-called **intra-coupled similarity** within an attribute. **Such couplings integrate the intra-coupled interactions within an
attribute and inter-coupled interactions among different attributes.**

Collaborative filtering (CF) is one of the most successful approaches taking advantage
of user rating history to predict users’ interests. As one of the most accurate single
models for collaborative filtering, matrix factorization (MF) is a latent factor model 
which generally effective at estimating overall structure that relates simultaneously to most items. 

![User-Item Table](http://i.imgur.com/VIvQYGa.png)
![CMFModel](http://i.imgur.com/quOc5nr.png)

## The contributions of the paper: ##
- A complete consideration of couplings may provide a practical mean for **enhancing the effectiveness** of RS.
- Especially, if we **do not have ample rating data**, the objective user coupling and item coupling can be utilized to make recommendations.

## Step ##
- We propose a coupled measure to capture the relationships for users and items,
namely user coupling and item coupling, which consider the coupled interaction
**between attributes** from non-IID perspective.
- We propose a Coupled Matrix Factorization (CMF) model by accommodating the
user coupling, item coupling and users’ subjective rating preferences together.

## CMF Algorithm##

- User Coupling

**Definition 1**. Formally, given user attribute space S<sub>u</sub> =< U,A,V,f >, the Coupled
User Similarity (CUS) between two users u<sub>i</sub> and <sub>j</sub> is defined as follows.
![CUS](http://i.imgur.com/tJhiQpN.png)

where V<sub>ik</sub> and V<sub>jk</sub> are the values of attribute k for users u<sub>i</sub> and u<sub>j</sub>, respectively; and δ<sup>Ia</sup><sub>k</sub> is the intra-coupling within attribute A<sub>k</sub>, δ<sup>Ie</sup><sub>k</sub> is the inter-coupling between different attributes.

- Item Coupling

**Definition 2**. Formally, given item attribute space S<sub>o</sub> =< U,A',V',f' >, the Coupled Item Similarity (CIS) between two items oi and oj is defined as follows.
![CIS](http://i.imgur.com/YTJ6eve.png)

where V <sup>′</sup><sub>ik</sub> and V <sup>′</sup><sub>jk</sub> are the values of attribute j for items o<sub>i</sub> and o<sub>j</sub>, respectively; and
δ<sup>Ia</sup><sub>k</sub> is the intra-coupling within attribute A<sub>k</sub>, δ<sup>Ie</sup><sub>k</sub> is the inter-coupling between different attributes.

- Coupled MF Model

MF approaches have been recognized as the main stream in RS through a latent topic
projection learning model. In this work, we attempt to incorporate all discussed couplings into a MF scheme. Traditionally, the matrix of predicted ratings R^ ∈ R<sup>n×m</sup>,
where n, m respectively denote the number of users and the number of items, can be
modeled as: R^ = r<sub>m</sub> + PQ<sup>T</sup> with matrices P ∈ R<sup>n×d</sup> and Q ∈ R<sup>m×d</sup>, where d is the rank (or dimension of the latent space) with d ≤ n,m, and r<sub>m</sub> ∈ R is a global offset value. Through this modelling, the prediction task of matrix R^ is transferred to compute the mapping of items and users to factor matrices P and Q. Once this mapping is completed, R^ can be easily reconstructed to predict the rating given by one user to an item.

In our proposed CMF, we take not only the rating matrix, but also the user coupling
and item coupling, into account. All these aspects should be accommodated into a unified learning model. The learning procedure is constrained by three-fold: the learned
rating values should be as close as possible to the observed rating values, the predicted user and item profiles should be similar to their neighbourhoods as well, which are
derived from their coupling information. Specifically, in order to incorporate the user
coupling and item coupling, we add two additional regularization factors in the optimization step. Then the computation of the mapping can be similarly optimized by
minimizing the regularized squared error. The objective function is given as Eqn.3.
![ObjectiveFunction](http://i.imgur.com/YYGdYVq.png)
As we can see in the objective function, the rating preference, user coupling and
item coupling have been all incorporated together. Specifically, the first part reflects
the subjective rating preferences and the latter two parts reflect the user coupling and
item coupling, respectively. This means when we recommend relevant items to users,
the users’ rating preferences may take the dominant role. Besides this, another distinct
advantage is that, when we do not have ample rating data, it is still possible to make satisfactory recommendations via leveraging the coupling information, e.g., one user will
be recommended what his/her neighbours like or items similar to what he/she preferred
before.

To optimize the above objective equation, we minimize the objective function L by
the **gradient descent** approach:
![gradientDescent](http://i.imgur.com/22NuHUe.png)
where I<sub>u,o<sub>i</sub></sub> is the function indicating that whether user has rated item o<sub>i</sub>, 1 means
rated, 0 means not rated. CUS(u,v) is the coupled similarity of users u and v, and CIS(o<sub>i</sub>,o<sub>j</sub>) is the coupled similarity of items o<sub>i</sub> and o<sub>j</sub>. N(u) and N(o<sub>i</sub>) respectively
represent the user and item neighborhood filtered by coupled similarity.

Model Training Through the above gradient descent approach, the best matrices P
and Q can be computed in terms of the user coupling, item coupling and user-item
coupling. The whole process of the coupled model starts at computing user coupling
and item coupling based on their objective attribute space, then neighbors of users and
items are selected from the couplings. Next, values of P and Q are randomly initiated
followed by an iteration step to update P and Q until convergence according to Eqn. 4
and 5. After P and Q are learned from the training process, we can predict the ratings
for user-item pairs (u,o<sub>i</sub>).

## Dataset ##
- [Movielens](http://www.movielens.org)

- [Bookcrossing](http://www.bookcrossing.com)

## Experimental Settings ##

How to verify:**5-fold cross validation** 

Evaluation parameter:Root Mean
Square Error (**RMSE**) &Mean Absolute Error (**MAE**)

Baseline approaches:

1. The basic probabilistic matrix factorization (**PMF**) approach;  

1. Singular value decomposition (**RSVD**) is a factorization method to decompose the rating matrix; 

1. Implicit social matrix factorization (**ISMF**) is an unified model
which incorporates implicit social relationships between users and between items computed by Pearson similarity based on the user-item rating matrix; 

1. User-based CF
(**UBCF**) first computes users’ similarity by Pearson Correlation on the rating matrix, then recommends relevant items to the given user according to the users who have
strong relationships; 

1. Item-based CF (**IBCF**) first considers items’ similarity by
Pearson Correlation on the rating matrix, then recommends relevant items which have strong relationships with the given user’s interested items.

1. **PSMF** 
use Pearson Correlation Coefficient to compute the relationships within users and items based on their attributes.The objective function of PSMF is similarly constructed as Eqn.3 by respectively replacing CUS(u,v), CIS(o<sub>i</sub>,o<sub>j</sub>) as the pearson similarity.

2. **CSMF** 
use Cosine similarity measures to compute the relationships within users and items based on their attributes.The objective function of CSMF is similarly constructed as Eqn.3 by respectively replacing CUS(u,v), CIS(o<sub>i</sub>,o<sub>j</sub>) as the pearson similarity.

3.**JSMF**
use Jaccard similarity measures to compute the relationships within users and items based on their attributes.The objective function of JSMF is similarly constructed as Eqn.3 by respectively replacing CUS(u,v), CIS(o<sub>i</sub>,o<sub>j</sub>) as the pearson similarity.


#Problem#
1、What does it mean?

![](http://i.imgur.com/d5P2K9f.png)

2、How intra-coupled and inter-coupled are used?Why two "))"?
![](http://i.imgur.com/B2Zm7DG.png)

3、How to calculate L？How to use gradient descent？












