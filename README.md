# Popular Songs From 2010-2019
This project analyzes elements of popular songs, such as the artist, the genre, the BPM, and the year they were released. It then uses the data collected to contrast the average BPM of each genre, find what percentage of songs belong to what genre, and finally answer the question of which artist had the most hit songs last decade. This project made use of PowerBI, R, and Excel. If you do not have PowerBI installed on your computer, the report is available in PDF though it is not interactive. The R code is available.
## Dataset
This project used data from https://www.datacamp.com/workspace/datasets/dataset-r-spotify-music.
## Data Cleansing
Fixed the accents in the names of artists that were wrongly displayed. Ex: Beyonc� into Beyoncé

Using R to group all subgenres into a more encompassing genre to improve readability. 
```R
library(tidyverse)
read = read.csv('C:\\Users\\bened\\Downloads\\datacamp_workspace_export_2022-12-16 17_04_46.csv')
read_1 = read %>% mutate(genre = fct_collapse(read$top.genre,
Pop =             c('pop', 'dance pop', 'electropop', 'boy band','canadian pop', 'electropop', 'barbadian pop', 'art pop',
                  'dance pop',  'neo mellow', 'australian pop', 'indie pop', 'colombian pop', 'acoustic pop', 'baroque
                  pop', 'candy pop', 'folk-pop', 'alaska indie', 'metropopolis','danish pop', 'hollywood', 'irish
                  singer-songwriter', 'escape room'),
              
Soul_RnB =        c('british soul', 'alternative r&b', 'canadian contemporary r&b'),

Techno_House =    c('big room', 'electro', 'complextro', 'house', 'australian dance', 'belgian edm', 'brostep',
                  'downtempo', 'edm', 'electro house', 'electronic trap', 'tropical house'), 
                  
Hip_Hop =         c('detroit hip hop', 'hip pop', 'atl hip hop', 'chicago rap', 'canadian hip hop', 'australian hip hop', 'hip hop'),
Latin =           c('canadian latin', 'latin'),
Other =           c('contemporary country', 'celtic rock')))
```
# Plotting Data
Used the ggplot2 library from tidyverse in R and plots from PowerBI to plot the data.
```R
ggplot(read_1, aes(x = as.integer(bpm))) + 
geom_histogram(aes(col = genre)) + 
facet_grid(~genre) + 
labs(x = "BPM (Beats per Minute)", y = "Number of Songs", title = "BPM per Muisc Genre")
```
![Rplot](https://user-images.githubusercontent.com/120809566/208265026-c2252300-f957-4d64-a7a7-e8bb009db160.png)

```R
ggplot(read_1, aes(x = as.integer(bpm), y = as.character(genre))) + 
geom_boxplot(aes(col = genre)) + 
labs(x = "BPM (Beats per Minute)", y = "Genre", title = "BPM Summary per Muisc Genre")
```
![Rplot01](https://user-images.githubusercontent.com/120809566/208265159-936d293c-9dae-4c9f-ba8e-93085818f33a.png)
