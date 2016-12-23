#An effective recommendation method for cold start new users using trust and distrust networks#
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

**Time: 2013**

**journal: Information Sciences(CCF:B)**

**Key words: Recommendation system, Collaborative filtering, Social network**

**Author: Chien Chin Chen, Yu-Hao Wan, Meng-Chieh Chung**

**Location: Department of Information Management, National Taiwan University, Taiwan**
## Why do we need RS ##
1、a substantial number of Internet users rely on information retrieved from the web to make purchasing decisions

2、the number of retrieved documents is sometimes too large for users to obtain
the desired information

3、that users are more likely to purchase **products** or **services**（e.g:a picture, a video clip, a book, a movie, a product review, or a service） if items relevant to their preferences are recommended

4、help users efficiently acquire information about desired items and thus motivate them to purchase

## What difficulty do we meet? ##
However, as new users require time to become familiar with recommendation
systems, the systems usually have **limited information about newcomers** and **have difficulty providing appropriate recommendations**.(new user cold start phenomenon)

collaborative filtering：This method is based on the concept that likeminded people prefer similar items and thus uses the information in a user’s profile to identify reference users whose tastes are similar to those of the target user. Recommendations are then made to the target user based on the items that interest
the reference users. （Amazon.com,Epinions.com）

##How do we solve the difficulty？##
1、The first type refines the similarity metrics used to identify effective reference users. （For instance, Ahn**[2]** defined the **PIP metric**, which measures the proximity, impact, and popularity of ratings, to resolve the rating sparsity problem of cold start new users and identify effective reference users. ）

2、The second type utilizes the **social relations** between users to identify reference users for cold start new users.(Since cold start new users do not know which users are trustworthy, limited (i.e., short) trust lists would degrade the quality of the recommendations for cold start new users.)

3、Our method.Ours analyzes the web of trust of experienced users to identify trustworthy users. The rating preferences of the trustworthy users are
then aggregated based on their reputation scores to recommend useful items for cold start new users. The method is implemented in two stages. 

First, we construct a user model by employing a **clustering algorithm** to group experienced users into clusters. The users in each cluster have similar item preferences. Rather than use the limited trust lists discussed above, the
proposed method suggests **trustworthy users** to cold start new users. We construct a web of trust for each cluster and utilize
the **PageRank algorithm** [25] to identify **experts** in a cluster. At the same time, we analyze the **distrust information** of each
cluster to screen out unreliable candidates. 

In the second stage, we compute the possible rating of an un-rated item for a cold start new user by first identifying the clusters closely related to the user. A cluster is deemed closely related to an item if several users in the cluster rate the item. We identify the **experts** of the clusters closely related to the un-rated item and the items rated by the cold start new user. The identified experts are exploited as reference users to make useful recommendations for the cold start new user. We also introduce a technique that identifies the **implicit links** between users in a web of trust. Although recommendation systems provide user-friendly interfaces for compiling trust lists, many users may be unwilling to use the function due to privacy concerns. The proposed technique resolves this problem by analyzing the rating behavior patterns of users and identifying instances of implicit trust to enrich the web of trust. 
##  review the selection techniques ##
- trustbased recommendation methods 
- new user cold start recommendation methods

Recommendation approaches: content-based filtering,collaborative filtering(item-based and **user-based**(memory-based and model-based))

1.content-based filtering

Examine the items rated by the target user.

e.g:content-based Personal View Agent(PVA) recommendation system([6]),text classification techniques to recommand([23])

2.collaborative filtering

In addition to the items rated by the target user, collaborative filtering approaches examine the items rated by other users.

1). memory-based

![MB](http://i.imgur.com/A9HHRS9.png)
![EX](http://i.imgur.com/pqlzNYi.jpg)
rating of i<sub>m</sub> given by user u<sub>j</sub>

similarity of users’ ratings for items: **correlation coefficient**>vector space similarity.

But the two method have a problem:rating sparsity problem

Solve:divides items into a set of classes.The preference of a user for a class is indicated by the user’s total rating for the items in that class. In addition, to measure the similarity between users, the authors apply the correlation coefficient to the class ratings. Since the number of classes is far smaller than the number of items, the metric mitigates the effect of the rating sparsity problem.

MB problem:
A major problem with memory-based approaches is the lack of scalability [16,43]. To identify similar users as reference users, a memory-based approach needs to record the item ratings of all users and run a database scan. However, due to the high expenses associated with the computation of a database scan, the scale of memory-based approaches is limited. 


2). model-based







## Dataset ##
[Epinions](http://www.trustlet.org/datasets/)
## Evaluation ##
recall rate, F1 score, coverage rate, users coverage rate, and execution time,







