# tweets_noon_analysis
- Author: Okugawa Tomoki（奥川 智貴）
- Date: 2022/05/02


## Intro
I investigated the question “When are time-related words such as "なう" used on Twitter?”.

I major in natural language processing and am interested in quantitatively analyzing Japanese words, so I decided to work on this question. 
"なう" is generally said to be informal Japanese used to describe the present.( "なう" is based on the English word "now".) 
However, it is not strictly defined as a word that refers to the current time.

Let's take a tweet containing "正午なう" posted at 12:05 as an example. Since "正午" is a time expression exactly at 12:00, "なう" in this tweet can be simply calculated as taking on the amount of time of 5 minutes(= 12:05 - 12:00). 

Based on this idea, to find out the amount of time that some time-related words mean, the following experiments were performed.

## Experiment Design
1. Dependent variable: WORD. Shown in the table below.

| WORD(variable name) | Japanese phrase |
| :-: | :-: |
| NAU | 正午なう |
| IMA | 今正午 |
| MADA | まだ正午 |
| MOU | もう正午 |
| ALL | 正午 |


2. Independent variable: GAP(=tweet timestamp – 12:00). GAP means the amount of time WORD has.
3. Data collection protocol:
    1. 	Collect a lot of tweets including "正午" using Twitter API. 
    2.	Calculate GAP value for each tweet. GAP value is equal to tweet timestamp minus 12:00. The unit of GAP value is second.
    3.	Collect GAP values for each WORD value and output to files. For example, the "NAU" data file consists only of GAP values in tweets containing Japanese Phrase ”正午なう”. The "ALL" data file consists of all GAP values in tweets.

4. Data analysis protocol
    1.	Create a boxplot with two axes, WORD and GAP, based on GAP values received from the data files.
    2.	Calculate the confidence intervals for the values observed for GAP. Confidence level is set to 95%, so alpha=0.05.
    3.	Compare the difference in results between WORD.

## Data collection
 I Executed the experiment following the data collection protocol. 

First, I collected 14,324 tweets including “正午” by running the script named “1_get_tweets_noon.ipynb”.
These tweets were stored in the file named “tweets_noon_20220427.csv”.

Then GAP value for each tweet was calculated and collected for each WORD value and output to "tweets_noon_ALL_gap.csv"(WORD=”ALL”),"tweets_noon_NAU_gap.csv"(WORD=”NAU”), "tweets_noon_MOU_gap.csv"(WORD=”MOU”),"tweets_noon_MADA_gap.csv"(WORD=”MADA”) and "tweets_noon_IMA_gap.csv"(WORD=”IMA”) respectively.
These steps were done by running the script named “2_gap_calculation.ipynb”.

## Data analysis
I analyzed the data obtained by running the script named "3_gap_analysis.ipynb".
The table below shows the number(=count), mean, and standard deviation(=sd) of each WORD value.

| WORD | count | mean | sd |
| -: | -: | -: | -: |
| NAU | 37 | 92.5 | 128.6 |
| IMA | 13 | 1737.2 | 4044.2 |
| MADA | 25 | 612.6 | 7967.1 |
| MOU | 174 | 6.3 | 1907.7 |
| ALL | 14324 | 2571.7 | 15751.9 |

The other figures(boxplots,...) are shown in "3_gap_analysis.ipynb".

## Findings
- When WORD = “NAU” or “MOU”, the mean of GAP values was very close to 0.
- When WORD = “ALL”, the mean of GAP values was almost 2400 seconds(=40 minutes) and quite far from 0.
- When WORD = “NAU”, the width of the confidence interval for GAP values was quite small. 
- When WORD = “MADA” or “IMA”, the width of the confidence interval for GAP values was quite large.
- Compared to the total number of tweets, the number of data for each WORD value was not very large.

## Conclusion
This experiment shows that tweets including “正午なう” or “もう正午” are often posted at a time close to noon. 
In particular, it was observed that “なう" has a strong role as a word that indicates the current time. 
Considering that tweets containing "正午" are often posted at a time away from noon, "なう" can be said to be used as a current time marker. 

As mentioned above, I am able to find some answers to the first question “When are time-related words such as "なう" used on Twitter?” 
In the future, the more tweets I collect, the more reliable my answer will be.


