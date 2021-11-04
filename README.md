---
title: 'Proposal'
author: "Jung Ho Suh"
output: html_document
---
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
  
  ***S&P INDEX and FINDING OUT ITS ETF'S PROFIT, RELIABILITY***
  
  ***The name(s) of team member(s)***
    Jung Ho Suh
    
  ***The link to the data source***
    Daily Prices of SPY(S&P500 ETF) - https://www.kaggle.com/pdquant/sp500-daily-19862018
    
    Closing price of Top Indexes - https://www.kaggle.com/omkarborikar/closing-price-of-indexes-time-series-data
    
    S&P 500 Daily Data - https://www.kaggle.com/myungchankim/sp-500-daily-data-19281230-to-20210919
    
  ***An overview of the dataset***
```{r}
#library(read_csv)
dailysandp <- read.csv('SPX_500_Data.csv')
sandpuntil11 <- read.csv('Index closing price from 1994 to 2021.csv')
spyprice <- read.csv('spx.csv')
str(dailysandp)
str(sandpuntil11)
str(spyprice)
```
  The dataset is comprised of open, high, low, close S&P index and it's volume. Spyprice has the closing price of SPY ETF.
  
  ***A brief plan for the exploratory analysis: What questions can be answered from the dataset?***
  
  My plan is to evaluate what stategy is the most effective. 
  
  1. Buying one S&P index ETF a week/month no matter what.
  
  2. Buy S&P index ETF when the index goes down 5 to 10% (correction)
  
  3. Buy S&P index ETF when the index goes down more than 10% (crash)
  
  4. Buy S&P index ETF when the index goes down more than 20% (crisis like dot com crash, Subprime mortage/Lehman Brothers crash)
  
  5. Mix of the 2,3,4 strategy like buy 1 more S&P index ETF in case 2, buy 2 in case 3, buy 3 in case 4.
  
  I will start evaluating after 1980s, because that is more than 10 years before the dot com bubble(1995). Also I'll evaluate the effectiveness of the strategy 1980-2021, 1990-2021, 2000-2021, 2010-2021, and 2015-2021.
Dot com bubble is 1995, Subprime mortage crisis is 2007-8, Covid is 2020, so I have a nice distribution of big market crash. 
I hope I can make an observation about when to invest more on S&P index ETF to have the most profit.

If the data is not good enough for S&P 500, I may switch this observation to NASDAQ, and its ETF QQQ. In this case, I believe I can evaluate the effectiveness of the leverage ETFs too such as QLD, and TQQQ. 
