# NBA Shot Data Midterm Challenge

Welcome to the NBA Shot Data Midterm Challenge! This competition is designed to test your skills in exploratory data analysis (EDA), clustering, machine learning, feature engineering, and data visualization. The goal is to analyze NBA shot data, uncover insights, and predict shot success. Below are the competition guidelines and tasks.

## Overview

In this midterm, you will:

1. Perform **exploratory data analysis**, visualize trends, and identify outliers.
2. **Cluster players** to create player profiles based on their shot attributes.
3. Build a **shot prediction model**, using machine learning (but no deep learning) with engineered features to improve accuracy.
4. Participate in a **visualization challenge** to explain insights through creative and informative visualizations.

Part 3 includes a **leaderboard** that ranks participants based on the performance of their prediction models. You get full credit for beating the **baseline accuracy score of 0.62**, and bonus points if you're ranked in the top 10.

## Submission Guidelines

*We expect you to work individually on this midterm.*

*The goal of this midterm is to give you an opportunity to learn these tools and practice using them. The grade you receive is somewhat secondary. Using GenAI to answer the questions will rob you of a very important learning and practice opportunity. For that reason we ask that you turn off GenAI autocomplete for any development environment you use.  You can use the course AI assistant for more general, peripheral help, for example to explain concepts. Your use of that tool is logged, just so you know. Do not use any other GenAI tools for the midterm.* 

For all parts, write code and accompanying analysis in the `ds701-fa24-midterm.ipynb`. Ensure that your analysis is detailed and presented in the manner of a professional report. For part 4 (prediction task), you also have to create a submission file for the [Kaggle competition](https://www.kaggle.com/t/6b1722486c10455f967352fbf62682b2). It should follow the format of `submission.csv` which has two columns: ID and SHOT_MADE.

## Tasks

### 1. Exploratory Analysis, Visualization, and Outlier Detection

This part involves discovering interesting patterns and outliers in the dataset. Use your data wrangling and visualization skills to answer questions.

Deliverables:

- See the notebook `ds701-fa24-midterm.ipynb` for specific questions to answer.
- Provide visualizations (e.g., histograms, box plots, heatmaps) that clearly illustrate your findings in the notebook, creating code cells as you like.

### 2. Player Clustering: Defining Player Profiles

For this task, you will apply clustering techniques to identify distinct player profiles based on their shooting behavior. You could use features like:

- **Shot Types**: `SHOT_TYPE`, `ACTION_TYPE`
- **Shot Success Rate**: `SHOT_MADE`
- **Shot Distance**: `SHOT_DISTANCE`

But you're not limited to these!

You can use clustering algorithms like **K-Means**, **Gaussian Mixture Models**, or others. What we want to see is an understanding of what the clusters say about the data.

Deliverables:

- **Cluster analysis**: Describe the player clusters and how they might correspond to properties about the players or shots they take.
- Provide **visual representations** of your clusters (e.g., scatter plots with labeled clusters).

Grading:

- Your analysis will be judged based on clarity, and the depth of the insights provided.

### 3. Prediction Task: Shot Success Modeling (No Deep Learning)

In this task, your goal is to predict whether a shot will be made (`SHOT_MADE`). You will build a machine learning model that predicts shot success based on a variety of features.

**Important Notes**:

You are NOT allowed to use deep learning methods!

You are encouraged to perform **feature engineering** to create new and useful features for your models.

Suggested Feature Engineering Ideas:

- **Spatial Features**: Derive the shot angle from the basket using `LOC_X`, `LOC_Y`.
- **Shot Difficulty**: Combine features such as `SHOT_DISTANCE`, `LOC_X`, `LOC_Y`, and `SHOT_TYPE` to create a new feature representing shot difficulty.
- **Player Fatigue**: Estimate player fatigue based on `GAME_DATE` (players are potentially more fatigued later in the season) and how late in the game the shot occurs (`MINS_LEFT`, `SECS_LEFT`).

Deliverables:

- A machine learning model that predicts shot success. Provide a summary of your model’s performance, including metrics like **accuracy**, **precision**, **recall**, or **F1-score**.
- **Feature engineering discussion**: Document any new features you created and how they improved your model.

Put the model summary and report into the notebook, no need for a separate document!

### 4. Visualization Challenge (BONUS)

In this challenge, we want you to go beyond basic visualizations. This is an opportunity to showcase your creativity and data storytelling abilities. This is an optional section but you can earn up to 5 bonus points.

Suggested Visualizations:

- **Shot Heatmap**: Create a heatmap showing shot success rates across different areas of the court for players or teams.

  - Example: _"Where are players most successful on the court?"_

- **Clutch Shot Analysis**: Analyze performance when the game is close or when time is running out.

  - Example: _"Which players perform well in high-pressure situations, such as late in the game?"_

## Dataset

The dataset contains the following columns:

```{python}
['SEASON_1', 'SEASON_2', 'TEAM_ID', 'TEAM_NAME', 'PLAYER_ID', 'PLAYER_NAME',
 'POSITION_GROUP', 'POSITION', 'GAME_DATE', 'GAME_ID', 'HOME_TEAM', 'AWAY_TEAM',
 'EVENT_TYPE', 'SHOT_MADE', 'ACTION_TYPE', 'SHOT_TYPE', 'BASIC_ZONE',
 'ZONE_NAME', 'ZONE_ABB', 'ZONE_RANGE', 'LOC_X', 'LOC_Y', 'SHOT_DISTANCE',
 'QUARTER', 'MINS_LEFT', 'SECS_LEFT']
```

## Resources

To make court visualizations easier, we've provided a function `draw_court` in the `utils.py` file. Could prove useful for Question 4 (Advanced Visualization)!

Here's an example of plotting Kobe Bryant's career shots:

```{python}
from utils import draw_court

bryant_id = 977 # Kobe Bryant
game_df = df[(df['PLAYER_ID'] == bryant_id)]

plt.figure(figsize=(8, 8))
# The 'game_df['LOC_X'] * 10 and (game_df['LOC_Y'] - 5) * 10' operations were chosen arbitrarily, we suggest you keep them.
plt.scatter(game_df['LOC_X'] * 10, (game_df['LOC_Y'] - 5) * 10, c=game_df['SHOT_MADE'], cmap='coolwarm', alpha=0.5)
draw_court(outer_lines=True, color="darkblue")

# These make sure the court is of a reasonable size
plt.xlim(-300, 300)
plt.ylim(-100, 500)

plt.axis('off')
plt.show()
```

## Grading

- **Exploratory Analysis and Visualizations** (10 pts): These will be graded on correctness and creativity.
  - Parts 1-6 are each 1 point.
  - Part 7 is worth 4 points. You will be graded on the quality of your description and the validity of your insight.
- **Clustering** (15 pts): Clustering will be evaluated based on the cohesion and separation of the clusters, as well as the accompanying discussion.
  - 5 pts for creating a valid clustering.
  - 5 pts for providing high quality visualizations of the clusters.
  - 5 pts for providing a clear interpretation and explanation of the clusters.
- **Prediction Task** (10 pts): The leaderboard will rank participants based on their model performance (e.g., accuracy) on a held-out test set.

  - 4 pts for creating and validating a model
  - 1 pt for beating the baseline score of 0.62
  - 5 pts for explanation of feature and model choices
  - 2 bonus pts for finishing top 10 in the leaderboard

- **Visualization** (3 possible bonus pts): To receive the full bonus credit you must provide a creative and informative visualization.

Good luck, and may the best analysis win!
