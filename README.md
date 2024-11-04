
# 🎵 Understanding Musical Trends: EDA on Spotify’s Most Streamed Songs of 2023

## Foreword

This project's objective is to examine song streaming trends on Spotify, a music platform, in 2023.

We initially examine the variables in the dataset to see if any are missing and what data types are being used before beginning the real analysis. Many important factors are highlighted, such as the total number of streams, the date of the song's release, and musical elements including danceability, beats per minute (BPM), and structure. 
Bar graphs and scatter plots, which reveal patterns and trends in time-series data, are other ways that data trends are displayed.

This section's questions aimed to investigate the connections between the streams and other musical elements like tempo and energy. 
Along with information on the factors that contributed to the song tracks' popularity, the report offers suggestions for recording artists, stakeholders, and other significant players in the music business. 

Therefore, the goal of this EDA is to shed light on the elements that contributed to Spotify streaming success in 2023.

> [!Note]
> 📖 Spotify[^1] is a digital music, podcast, and video service that gives you access to millions of songs and other content from creators all over the world.

[^1]: https://support.spotify.com/uk/article/what-is-spotify/

---

## Content

- **[Loading the Dataset](#loading-the-dataset)**

- **[Overview of Dataset](#overview-of-dataset)**

- **[Basic Descriptive Statistics](#basic-descriptive-statistics)**

- **[Top Performers](#top-performers)**

- **[Temporal Trends](#temporal-trends)**

- **[Genre and Music Characteristics](#genre-and-music-characteristics)**

- **[Platform Popularity](#platform-popularity)**

- **[Advanced Analysis](#advanced-analysis)**

---

## Loading the Dataset
- Before doing the analysis and interpretation of data, import first the libraries that will be used which are pandas, matplot, and seaborn.

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

- After that is done load the data set using `pd.read_csv()`

🌱 Input:
```python
# reading the csv, loading the dataset
spotify = 'spotify-2023.csv'
df = pd.read_csv(spotify, encoding='ISO-8859-1')
# printing the dataset
df
```
🌳 Output:
<table>
  <tr>
    <th></th>
    <th>track_name</th>
    <th>artist(s)_name</th>
    <th>artist_count</th>
    <th>released_year</th>
    <th>released_month</th>
    <th>released_day</th>
    <th>in_spotify_playlists</th>
    <th>in_spotify_charts</th>
    <th>streams</th>
    <th>in_apple_playlists</th>
    <th>...</th>
    <th>bpm</th>
    <th>key</th>
    <th>mode</th>
    <th>danceability_%</th>
    <th>valence_%</th>
    <th>energy_%</th>
    <th>acousticness_%</th>
    <th>instrumentalness_%</th>
    <th>liveness_%</th>
    <th>speechiness_%</th>
  </tr>
  <tr>
    <td>0</td>
    <td>Seven (feat. Latto) (Explicit Ver.)</td>
    <td>Latto, Jung Kook	</td>
    <td>2</td>
    <td>2023</td>
    <td>7</td>
    <td>14</td>
    <td>553</td>
    <td>147</td>
    <td>141381703	</td>
    <td>43</td>
    <td>...</td>
    <td>125</td>
    <td>B</td>
    <td>Major</td>
    <td>80</td>
    <td>89</td>
    <td>83</td>
    <td>31</td>
    <td>0</td>
    <td>8</td>
    <td>4</td>
  </tr>
 <tr>
   <td>1</td>
    <td>LALA</td>
    <td>Myke Towers</td>
    <td>1</td>
    <td>2023</td>
    <td>3</td>
    <td>23</td>
    <td>1474</td>
    <td>48</td>
    <td>133716286	</td>
    <td>48</td>
    <td>...</td>
    <td>92</td>
    <td>C#</td>
    <td>Major</td>
    <td>71</td>
    <td>61</td>
    <td>74</td>
    <td>7</td>
    <td>0</td>
    <td>10</td>
    <td>4</td>
  </tr>
 <tr>
    <td>2</td>
    <td>vampire</td>
    <td>Olivia Rodrigo</td>
    <td>1</td>
    <td>2023</td>
    <td>6</td>
    <td>30</td>
    <td>1397</td>
    <td>113</td>
    <td>140003974	</td>
    <td>94</td>
    <td>...</td>
    <td>138</td>
    <td>F</td>
    <td>Major</td>
    <td>51</td>
    <td>32</td>
    <td>53</td>
    <td>17</td>
    <td>0</td>
    <td>31</td>
    <td>6</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Cruel Summer</td>
    <td>Taylor Swift</td>
    <td>1</td>
    <td>2019</td>
    <td>8</td>
    <td>23</td>
    <td>7858</td>
    <td>100</td>
    <td>800840817	</td>
    <td>116</td>
    <td>...</td>
    <td>170</td>
    <td>A</td>
    <td>Major</td>
    <td>55</td>
    <td>58</td>
    <td>72</td>
    <td>11</td>
    <td>0</td>
    <td>11</td>
    <td>15</td>
  </tr>
  <tr>
    <td>4</td>
    <td>WHERE SHE GOES</td>
    <td>Bad Bunny</td>
    <td>1</td>
    <td>2023</td>
    <td>5</td>
    <td>18</td>
    <td>3133</td>
    <td>50</td>
    <td>303236322	</td>
    <td>84</td>
    <td>...</td>
    <td>144</td>
    <td>A</td>
    <td>Minor</td>
    <td>65</td>
    <td>23</td>
    <td>80</td>
    <td>14</td>
    <td>63</td>
    <td>11</td>
    <td>6</td>
  </tr>
  <tr>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
    <td>...</td>
  </tr>
  <tr>
    <td>948</td>
    <td>My Mind & Me</td>
    <td>Selena Gomez</td>
    <td>1</td>
    <td>2022</td>
    <td>11</td>
    <td>3</td>
    <td>953</td>
    <td>0</td>
    <td>91473363	</td>
    <td>61</td>
    <td>...</td>
    <td>144</td>
    <td>A</td>
    <td>Major</td>
    <td>60</td>
    <td>24</td>
    <td>39</td>
    <td>57</td>
    <td>0</td>
    <td>8</td>
    <td>3</td>
  </tr>
  <tr>
    <td>949</td>
    <td>Bigger Than The Whole Sky</td>
    <td>Taylor Swift</td>
    <td>1</td>
    <td>2022</td>
    <td>10</td>
    <td>21</td>
    <td>1180</td>
    <td>0</td>
    <td>121871870</td>
    <td>4</td>
    <td>...</td>
    <td>166</td>
    <td>F#</td>
    <td>Major</td>
    <td>42</td>
    <td>7</td>
    <td>24</td>
    <td>83</td>
    <td>1</td>
    <td>12</td>
    <td>6</td>
  </tr>
  <tr>
    <td>950</td>
    <td>A Veces (feat. Feid)</td>
    <td>Feid, Paulo Londra</td>
    <td>2</td>
    <td>2022</td>
    <td>11</td>
    <td>3</td>
    <td>573</td>
    <td>0</td>
    <td>73513683</td>
    <td>2</td>
    <td>...</td>
    <td>92</td>
    <td>C#</td>
    <td>Major</td>
    <td>80</td>
    <td>81</td>
    <td>67</td>
    <td>4</td>
    <td>0</td>
    <td>8</td>
    <td>6</td>
  </tr>
  <tr>
    <td>951</td>
    <td>En La De Ella</td>
    <td>Feid, Sech, Jhayco</td>
    <td>3</td>
    <td>2022</td>
    <td>10</td>
    <td>20</td>
    <td>1320</td>
    <td>0</td>
    <td>133895612</td>
    <td>29</td>
    <td>...</td>
    <td>97</td>
    <td>C#</td>
    <td>Major</td>
    <td>82</td>
    <td>67</td>
    <td>77</td>
    <td>8</td>
    <td>0</td>
    <td>12</td>
    <td>5</td>
  </tr>
  <tr>
    <td>952</td>
    <td>Alone</td>
    <td>Burna Boy</td>
    <td>1</td>
    <td>2022</td>
    <td>11</td>
    <td>4</td>
    <td>782</td>
    <td>2</td>
    <td>96007391</td>
    <td>27</td>
    <td>...</td>
    <td>90</td>
    <td>E</td>
    <td>Minor</td>
    <td>61</td>
    <td>32</td>
    <td>67</td>
    <td>15</td>
    <td>0</td>
    <td>11</td>
    <td>5</td>
  </tr>
</table>
953 rows × 24 columns

---

> [!Tip]
> `encoding='ISO-8859-1'` was used because ISO-8859[^2] is a family of single-byte encoding schemes used to represent alphabets that can be represented within the range of 127 to 255. These various alphabets are defined as "parts" in the format ISO-8859-n, the most familiar of these likely being ISO-8859-1 aka 'Latin-1'.

**Further Explanation:**

When loading a csv file there are some accented characters, special symbols, etc. that may cause an error when reading the the dataset. In this case when the file contains noN-UTF-8 characters the `ISO 8859-1` encoding is used.

[^2]: https://stackoverflow.com/questions/7048745/what-is-the-difference-between-utf-8-and-iso-8859-1

---

## Overview of Dataset
1. How many rows and columns does the dataset contain?
- To find the rown and column of the dataset use the code `.shape`

🌱 Input:

```python
#get the size of the dataset
shape = df.shape
print(f"The dataset has {shape[0]} rows and {shape[1]} columns.")
```

🌳Output:

The dataset has 953 rows and 24 columns.

> [!Tip]
> Upon using the `.shape` code, it will automatically get the rows and columns, and using the print function will show the results of the said code. The `.shape` returns a tuple with each index having the number of corresponding elements[^3]. 

[^3]: https://www.w3schools.com/python/numpy/numpy_array_shape.asp

<br>

2. What are the data types of each column? Are there any missing values?

🌱 Input:
``` python
# getting the summary of the dataset
df.info()
```

🌳 Output:
<class 'pandas.core.frame.DataFrame'>

RangeIndex: 953 entries, 0 to 952

Data columns (total 24 columns):

| # | Column | Non-Null Count |  Dtype |
| ------------- | ------------- | -------------- | ----------- |
|0|  track_name  | 953 non-null   | object |
|1|  artist(s)_name | 953 non-null  |  object |
|2|  artist_count | 953 non-null  | int64|
|3|  released_year | 953 non-null  |  int64 |
|4|  released_month | 953 non-null  |  int64 |
|5|  released_day | 953 non-null  |  int64 |
|6|  in_spotify_playlists | 953 non-null  |  int64 |
|7|  in_spotify_charts | 953 non-null  |  int64 |
|8|  streams | 953 non-null  |  object |
|9|  in_apple_playlists | 953 non-null  |  int64 |
|10|  in_apple_charts | 953 non-null  |  int64 |
|11|  in_deezer_playlists | 953 non-null  |  object |
|12|  in_deezer_charts | 953 non-null  |  int64 |
|13|  in_shazam_charts | 903 non-null  |  object |
|14|  bpm | 953 non-null  |  int64 |
|15|  key | 858 non-null  |  object |
|16|  mode | 953 non-null  |  object |
|17|  danceability_% | 953 non-null  |  int64 |
|18|  valence_% | 953 non-null  |  int64 |
|19|  energy_% | 953 non-null  |  int64 |
|20|  acousticness_% | 953 non-null  |  int64 |
|21|  instrumentalness_% | 953 non-null  |  int64 |
|22|  liveness_% | 953 non-null  |  int64 |
|23|  speechiness_% | 953 non-null  |  int64 |

dtypes: int64(17), object(7)

memory usage: 178.8+ KB

**Explanation:**
To explain the results above, there are a total of 24 columns that are related to the music tracks. Each column represents something in the given dataset. Although in_shazam_charts has 903 non-null entry and key has 858 non-null entries which means that both of these columns contains missing data/entries, most of it contains 953 non-null entries which means that those columns have complete data for all entries. There are also 7 object columns which hold textual information and 17 integer columns which holds numerical data.

> [!Tip]
> The `.info()` function prints information about the DataFrame.[^4] The information contains the number of columns, column labels, column data types, memory usage, range index, and the number of cells in each column (non-null values).

[^4]:https://www.w3schools.com/python/pandas/ref_df_info.asp

---

## Basic Descriptive Statistics

- Before getting the mean, median, and standard deviation, use the code `.describe()` first to get the summary of the statistics for each numeric column in the dataset.

🌱 Input:
```python
# to get the summary of numerical values in the dataset
df.describe().round(4)
```

🌳 Output:

| | artist_count | released_year | released_month | released_day | in_spotify_playlists | in_spotify_charts | in_apple_playlists | in_apple_charts | in_deezer_charts | bpm | danceability_% | valence_% | energy_% | acousticness_% | instrumentalness_% | liveness_% | speechiness_% |
| -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| **count** | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 | 953.0000 |
| **mean** |	1.5561	| 2018.2382 |	6.0336 |	13.9307 |	5200.1249 |	12.0094 |	67.8122 |	51.9087 |	2.6663 |	122.5404 |	66.9696 |	51.4313	| 64.2791 |	27.0577 |	1.5813 |	18.2130 |	10.1312 |
| **std** |	0.8930 |	11.1162 |	3.5664 |	9.2019 |	7897.6090 |	19.5760 |	86.4415 |	50.6302 |	6.0356 |	28.0578 |	14.6306 |	23.4806 |	16.5505 |	25.9961 |	8.4098 |	13.7112 |	9.9129 |
| **min** |	1.0000 |	1930.0000 |	1.0000 |	1.0000 |	31.0000 |	0.0000 |	0.0000 |	0.0000 |	0.0000 |	65.0000 |	23.0000 |	4.0000 |	9.0000 |	0.0000 |	0.0000 |	3.0000 |	2.0000 |
| **25%** |	1.0000 |	2020.0000 |	3.0000 |	6.0000 |	875.0000 |	0.0000 |	13.0000 |	7.0000 |	0.0000 |	100.0000 |	57.0000 |	32.0000 |	53.0000 |	6.0000 |	0.0000 |	10.0000 |	4.0000 |
| **50%** |	1.0000 |	2022.0000 |	6.0000 |	13.0000 |	2224.0000 |	3.0000 |	34.0000 |	38.0000 |	0.0000 |	121.0000 |	69.0000 |	51.0000 |	66.0000 |	18.0000 |	0.0000 |	12.0000 |	6.0000 |
| **75%** |	2.0000 |	2022.0000 |	9.0000 |	22.0000 |	5542.0000 |	16.0000 |	88.0000 |	87.0000 |	2.0000 |	140.0000 |	78.0000 |	70.0000 |	77.0000 |	43.0000 |	0.0000 |	24.0000 |	11.0000 |
| **max** |	8.0000 |	2023.0000 |	12.0000 |	31.0000 |	52898.0000 |	147.0000 |	672.0000 |	275.0000 |	58.0000 |	206.0000 |	96.0000 |	97.0000 |	97.0000 |	97.0000 |	91.0000 |	97.0000 |	64.0000 |

1. What are the mean, median, and standard deviation of the streams column?
- To find the mean, median, and standard deviation, we can use the code `.mean()` for the mean, `.meadian()` for the median, and `.std()` for the standard deviation.
  
🌱 Input:
```python
# converts the values in the strems columns to number and replaces the non-numbers to NaN 
df['streams'] = pd.to_numeric(df['streams'], errors='coerce')
#removes the Nan values
df = df.dropna(subset=['streams'])
# calculates the mean
df['streams'].mean()
```

🌳 Output:

514137424.93907565

<br>

🌱 Input:
``` python
# calculates the median
df['streams'].median()
```

🌳 Output:
290530915.0

<br>
  
🌱 Input:
``` python
# calculates the standard deviation
df['streams'].std()
```

🌳 Output:

566856949.0388832

<br>

2. What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?

🌱 Input:
``` python
# Setting the size of the figure
plt.figure(figsize=(14, 6))

# Plotting the distribution of the released_year
plt.subplot(1, 2, 1)  # 1 row, 2 columns, 1st plot
plt.hist(df['released_year'],  color='red', edgecolor='white')  # Histogram
plt.title('The Distribution of Released Year')  # Title for the plot
plt.xlabel('Year')  # X-axis label
plt.ylabel('Frequency')  # Y-axis label

# Plotting the distribution of the artist_count
plt.subplot(1, 2, 2)  # 1 row, 2 columns, 2nd plot
plt.hist(df['artist_count'],  color='pink', edgecolor='white')  # Histogram
plt.title('The Distribution of Artist Count')  # Title for the plot
plt.xlabel('Number of Artists')  # X-axis label
plt.ylabel('Frequency')  # Y-axis label

# Displaying the plots
plt.show()
``
🌳 Output:


---

## Top Performers
1. Which track has the highest number of streams? Display the top 5 most streamed tracks.

2. Who are the top 5 most frequent artists based on the number of tracks in the dataset?


---

## Temporal Trends
1. Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.

2. Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?


---

## Genre and Music Characteristics
1. Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?

2. Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?


---

## Platform Popularity
1. How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?


---

## Advanced Analysis
1. Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?

2. Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.


---

