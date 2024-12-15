Dataset link: https://www.kaggle.com/datasets/tamber/steam-video-games/data

Task is to build a recommender system that can recommend games to a user based on their preferences using different approaches.

1. Understanding the User-Game Interaction Matrix
The matrix represents how much time each user has spent playing different games. Rows correspond to users, columns to games, and values indicate the number of hours played. For example:

User ID	Skyrim	Fallout 4	Spore
151603712	273.0	87.0	14.9
123456789	0.0	42.0	0.0
If a user has not interacted with a game, the value is 0.

2. Item-Based Collaborative Filtering
The system looks at similarities between games to recommend new games to a user based on the games they've already played.

a) Game Similarity
Cosine Similarity is used to measure how similar two games are based on users' play patterns. For example:
If many users who play Skyrim also play Fallout 4, these two games will have a high similarity score.
Cosine similarity is calculated as:
Similarity
(
𝐴
,
𝐵
)
=
A
⋅
B
∥
A
∥
∥
B
∥
Similarity(A,B)= 
∥A∥∥B∥
A⋅B
​
 
where 
𝐴
A and 
𝐵
B are the columns (games) in the interaction matrix.
b) Similarity Matrix
This creates a matrix showing how similar each game is to every other game:

Game	Skyrim	Fallout 4	Spore
Skyrim	1.0	0.85	0.34
Fallout 4	0.85	1.0	0.22
Spore	0.34	0.22	1.0
Diagonal values are 1 because each game is perfectly similar to itself.

3. Generating Recommendations
a) For a Specific User
Find Played Games: Identify the games the user has already played (non-zero values in the matrix).

Example: User 151603712 has played Skyrim (273.0 hours) and Fallout 4 (87.0 hours).
Aggregate Similarity Scores: Sum up the similarity scores for all unplayed games, weighted by the similarity to the played games:

Score
(
𝐺
𝑎
𝑚
𝑒
)
=
∑
Played Games
Similarity
(
𝐺
𝑎
𝑚
𝑒
,
𝑃
𝑙
𝑎
𝑦
𝑒
𝑑
𝐺
𝑎
𝑚
𝑒
)
Score(Game)= 
Played Games
∑
​
 Similarity(Game,PlayedGame)
For example:

If Spore has a similarity of 0.34 to Skyrim and 0.22 to Fallout 4, its total score might be 
0.34
+
0.22
=
0.56
0.34+0.22=0.56.
Exclude Played Games: Ignore games the user has already played to recommend only new games.

Rank and Recommend: Sort the unplayed games by their aggregated scores and recommend the top N.
