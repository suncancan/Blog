#An effective recommendation method for cold start new users using trust and distrust networks#

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







