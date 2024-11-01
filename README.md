
# 🎵 Understanding Musical Trends: EDA on Spotify’s Most Streamed Songs of 2023**

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

- **[Overview of Dataset](#overview-of-dataset)**

- **[Basic Descriptive Statistics](#basic-descriptive-statistics)**

- **[Top Performers](#top-performers)**

- **[Temporal Trends](#temporal-trends)**

- **[Genre and Music Characteristics](#genre-and-music-characteristics)**

- **[Platform Popularity](#platform-popularity)**

- **[Advanced Analysis](#advanced-analysis)**

---

## Loading the Dataset
- Before doing the analysis and interpretation of data, load the data set first using `pd.read_csv()`

🌱 Input:
```python
spotify = 'spotify-2023.csv'
df = pd.read_csv(spotify, encoding='ISO-8859-1')
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


2. What are the data types of each column? Are there any missing values?

---

## Basic Descriptive Statistics
1. What are the mean, median, and standard deviation of the streams column?
- To find the mean, median, and standards deviation we can use the code `.mean()` for the mean, `.meadian()` for the median, and `.std()` for the standard deviation.
🌱 Input:
```python

```
  
2. What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?


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

























