# tweets_noon_analysis
## Intro
    I investigated the question “When are time-related words such as "なう" used on Twitter?”
I major in natural language processing and am interested in quantitatively analyzing Japanese words, so I decided to work on this question. "なう" is generally said to be informal Japanese used to describe the present.( "なう" is based on the English word "now".) However, it is not strictly defined as a word that refers to the current time.

Let's take a tweet containing "正午なう" posted at 12:05 as an example. Since "正午" is a time expression exactly at 12:00, "なう" in this tweet can be simply calculated as taking on the amount of time of 5 minutes(= 12:05 - 12:00). 

Based on this idea, to find out the amount of time that some time-related words mean, I Created and executed this programs.

## Data collection protocol
1.	Collect a lot of tweets including "正午" using Twitter API. 
2.	Calculate GAP value for each tweet. GAP value is equal to tweet timestamp minus 12:00. The unit of GAP value is second.
3.	Collect GAP values for each WORD value and output to files. For example, the "NAU" data file consists only of GAP values in tweets containing Japanese Phrase ”正午なう”. The "ALL" data file consists of all GAP values in tweets.

## Data analysis protocol
1.	Create a boxplot with two axes, WORD and GAP, based on GAP values received from the data files.
2.	Calculate the confidence intervals for the values observed for GAP. Confidence level is set to 95%, so alpha=0.05.
3.	Compare the difference in results between WORD.

## Data collection
  I Executed the experiment following the data collection protocol. 

First, I collected 14,324 tweets including “正午” by running the script named “1_get_tweets_noon.ipynb”.
These tweets were stored in the file named “tweets_noon_20220427.csv”.

Then GAP value for each tweet was calculated and collected for each WORD value and output to "tweets_noon_ALL_gap.csv"(WORD=”ALL”),"tweets_noon_NAU_gap.csv"(WORD=”NAU”), "tweets_noon_MOU_gap.csv"(WORD=”MOU”),"tweets_noon_MADA_gap.csv"(WORD=”MADA”) and "tweets_noon_IMA_gap.csv"(WORD=”IMA”) respectively.
These steps were done by running the script named “2_gap_calculation.ipynb”.
