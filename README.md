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
![Rplot01](https://user-images.githubusercontent.com/120809566/208265342-481124bd-3665-41b4-87d9-e71b24f9a4a9.png)

```R
ggplot(read_1, aes(x = as.integer(bpm), y = as.character(genre))) + 
geom_boxplot(aes(col = genre)) + 
labs(x = "BPM (Beats per Minute)", y = "Genre", title = "BPM Summary per Muisc Genre")
```
![Rplot05](https://user-images.githubusercontent.com/120809566/208265361-1a02acec-d2e6-4ce2-a6b7-df3a328f5a3f.png)


```R
ggplot(read_1,aes(x=as.integer(year),fill=genre)) +
geom_bar() + scale_fill_viridis_d() + labs(x = "Year", y = "Number of Songs", title = "Proportion of Songs per Year")
```
![Rplot02](https://user-images.githubusercontent.com/120809566/208265398-506ff252-ea4f-4775-8c00-cd460ce156bd.png)


```R
ggplot(read_1,aes(x="",y="", fill=genre)) + 
geom_bar(stat="identity") + coord_polar("y",start=0) + 
theme(axis.title.y =element_blank(), axis.text.y =element_blank(), axis.ticks.y=element_blank()) + 
labs(title = "Genres of The Top Songs From 2010-2019")
```
![Rplot03](https://user-images.githubusercontent.com/120809566/208265413-9fa7cd63-7215-4f3d-b53f-04bb1f89a633.png)


```R
ggplot(read_1,aes(x=genre,fill=genre)) + geom_bar() + scale_fill_viridis_d() + 
labs(x = 'Genre', y = 'Number of Songs', title = "Genres of The Top Songs From 2010-2019") 
```
![Rplot04](https://user-images.githubusercontent.com/120809566/208265464-da7d4115-23ca-4736-a8d4-9e504fac0c26.png)

# PowerBI Plots With The R Plots, and the Summary of Each Analaysis
![Analysis of Popular Songs From 2010 - 2019-1](https://user-images.githubusercontent.com/120809566/208265542-ecf8fb15-85ac-41ce-bcfd-bdce80acb02b.png)
![Analysis of Popular Songs From 2010 - 2019-3](https://user-images.githubusercontent.com/120809566/208265543-b437a70f-b214-40bf-81a7-be2ad94e8cc9.png)
![Analysis of Popular Songs From 2010 - 2019-2](https://user-images.githubusercontent.com/120809566/208265547-02bc2ae8-17be-4cbf-9464-632e785e0926.png)
