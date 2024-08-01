# Songs Recommendation System

This project is a songs recommendation system that utilizes clustering techniques to group songs based on their features and then recommends similar songs.

## Table of Contents
- [Introduction](#introduction)
- [Dataset](#dataset)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Modeling](#modeling)
- [Recommendation System](#recommendation-system)
- [Installation](#installation)
- [Usage](#usage)


## Introduction
The Songs Recommendation System clusters songs using features like `acousticness`, `valence`, and `liveness`. The system then recommends songs similar to a given input song based on the Euclidean distance between their features.

## Dataset
The dataset used for this project contains information about songs, including features such as `acousticness`, `valence`, `liveness`, and more.

### Reading the Dataset
The dataset is read from a CSV file using Pandas.

```python
df = pd.read_csv("path/to/songs.csv")
df.info()
```
## Exploratory Data Analysis
Several analyses were performed to understand the distribution and clustering potential of the data:

 - **Histogram of Songs per Album**: Visualized using Matplotlib and Seaborn.
 - **Elbow Method**: Used to determine the optimal number of clusters for K-Means clustering based on acousticness and valence.
 - **Silhouette Score Analysis**: Evaluated clustering performance for different numbers of clusters.
## Modeling
The K-Means clustering algorithm was used to group songs into clusters based on their features:

- **Two Features (acousticness and valence):**
   - Optimal number of clusters determined using the elbow method and silhouette scores.
   - Model fitting and prediction performed.
   - Results visualized using scatter plots.
- **Three Features (acousticness, valence, and liveness):**
  - Similar steps followed as above for three features.
## Recommendation System
A recommendation function was implemented to suggest songs similar to a given song. The Euclidean distance between the features of the songs was used to find the closest match.
```python
def song_recommendation(name, df):
    recommend = []
    a = np.array(df.loc[df['song'] == name][['acousticness', 'valence', 'liveness']]).flatten()
    for num in df['id']:
        b = np.array(df.loc[df['id'] == num][['acousticness', 'valence', 'liveness']]).flatten()
        c = distance.euclidean(a, b)
        recommend.append([df.loc[df['id'] == num]['song'], c])
        recommend.sort(key=lambda x: x[1])
    return recommend[1]
```
## Installation
To run this project, you'll need the following libraries:

 - pandas
 - numpy
 - matplotlib
 - seaborn
 - plotly
 - scikit-learn
 - scipy
## Usage
To use the recommendation system, call the song_recommendation function with the name of a song and the dataset:
```python
song_recommendation(song_name, df)
```






