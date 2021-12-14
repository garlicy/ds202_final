---
title: 'Project Report'
author: "Jung Ho Suh"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
  
***Evaluating ETFs' Performance and Stability***
  
***The name(s) of team member(s)***
    Jung Ho Suh
    
***The link to the data source***

    SPY Dataset
    https://finance.yahoo.com/quote/SPY/history/
    
    QQQ Dataset
    https://finance.yahoo.com/quote/QQQ/history/
    
    TQQQ Dataset
    https://finance.yahoo.com/quote/TQQQ/history/
    
    Portfolio Visualizer
    https://www.portfoliovisualizer.com/
    
***Background Information***

There are two famous and popular index to evaluate the stock market. NASDAQ and S&P 500. NASDAQ-National Association of Securities Dealers Automated Quotations is one of the biggest stock exchange in the world, and it primarily focuses on IT companies and other growing stocks.
S&P 500-Standard and Poor's 500 is a stock market index that tracks 500 biggest publicly traded companies. Compared to NASDAQ, it has more sectors other than IT related, and it is often used as the best index to evaluate the whole stock market.

ETF stands for exchange-traded fund. Unlike the normal funds that are run by financial companies such as Blackrock, ETFs are able to be traded in the stock market like other stocks. One of the most popular variants of ETFs is the index ETF, which tracks the specific index. For our cause, we are going to use NASDAQ and S&P500 indexes, and their tracking ETFs.

**NASDAQ ETF**

*QQQ*

*TQQQ*

**S&P500 ETF**

*SPY*

**QQQ and TQQQ are run by Invesco. SPY is run by Standard&Poors.**

Recent stock market boom after the COVID-19, has encouraged many people to look into stocks. One of the most popular stock was Tesla (TSLA) because of its steep growth.It surged 740% in 2020 year alone. Recently, Gamestop (GME) and Lucid Motors (LCID) were the most viral stocks in the market, booming more than 500% in less than two months.

It is good to earn money by investing in those "meme" stocks, however, the more important thing in stock market in my opinion, is not losing the money. 

If you believe in the United States continuous growth in the future, you should look into index ETFs, since it is essentially investing the money into the most famous, popular, renown companies in the United States. 

**The question is "how to invest into the index ETF wisely?"**

For the most basic and simple strategy in investing stocks is that to put the same amount of money no matter by the same duration. Just like saving money in the savings account, you put your money into the index tracking ETFs. The difference of index ETFs to normal savings account is that it has a potential to yield much more profit. Unlike savings account that ensures up to 2% interest rate which barely covers inflation rate, investing in the index ETFs, often results in more than 100%, which means the money doubled in an year. There is one disadvantage, that it does not guarantee the amount of money, so there is a risk to lose your money. However, since the United States is the largest in the world economically, and has Dollar as worldwide currency, and its ever-continous growth due to endless innovations, it is safe to say that probability of losing the money in index ETFs is considerably low. 

For NASDAQ tracking ETF, we are going to test our stategy in trading *QQQ*, and *TQQQ*, the triple leveraged version of *QQQ*. Both are run by Invesco. Triple Leveraged ETF meaning simply put is that you get the profit three times, but also take the crash three times too.

For S&P500 tracking ETF, we are going to use *SPY*, the largest and oldest index ETF ever traded. It is run by Standard and Poor's


Let's explore the data now.

```{r}
if(!require("readxl")) install.packages("readxl",repos = "http://cran.us.r-project.org")
if(!require("dplyr")) install.packages("dplyr",repos = "http://cran.us.r-project.org")
if(!require("tidyr")) install.packages("tidyr",repos = "http://cran.us.r-project.org")
if(!require("ggplot2")) install.packages("ggplot2",repos = "http://cran.us.r-project.org")
if(!require("gridExtra")) install.packages("gridExtra",repos = "http://cran.us.r-project.org")
if(!require("cowplot")) install.packages("cowplot",repos = "http://cran.us.r-project.org")


library(readxl)
library(gridExtra)
library(cowplot)

dailySPY <- read.csv('SPY.csv')
dailyQQQ <- read.csv('QQQ.csv')
dailyTQQQ <- read.csv('TQQQ.csv')

annual_QQQ_2000 <- read_excel('edit_QQQ_2000_Portfolio.xlsx', sheet='Annual Return')
annual_QQQ_2011 <- read_excel('edit_QQQ_2011_Portfolio.xlsx', sheet='Annual Return')
annual_TQQQ_2011 <- read_excel('edit_TQQQ_2011_Portfolio.xlsx', sheet='Annual Return')
annual_SPY_2000 <- read_excel('edit_SPY_2000_Portfolio.xlsx', sheet='Annual Return')

monthly_QQQ_2000 <- read_excel('edit_QQQ_2000_Portfolio.xlsx', sheet='Monthly Return')
monthly_QQQ_2011 <- read_excel('edit_QQQ_2011_Portfolio.xlsx', sheet='Monthly Return')
monthly_TQQQ_2011 <- read_excel('edit_TQQQ_2011_Portfolio.xlsx', sheet='Monthly Return')
monthly_SPY_2000 <- read_excel('edit_SPY_2000_Portfolio.xlsx', sheet='Monthly Return')

crash_QQQ_2000 <- read_excel('edit_QQQ_2000_Portfolio.xlsx', sheet='Historical Crash')
crash_QQQ_2011 <- read_excel('edit_QQQ_2011_Portfolio.xlsx', sheet='Historical Crash')
crash_TQQQ_2011 <- read_excel('edit_TQQQ_2011_Portfolio.xlsx', sheet='Historical Crash')
crash_SPY_2000 <- read_excel('edit_SPY_2000_Portfolio.xlsx', sheet='Historical Crash')

drawdown_QQQ_2000 <- read_excel('edit_QQQ_2000_Portfolio.xlsx', sheet='Drawdown')
drawdown_QQQ_2011 <- read_excel('edit_QQQ_2011_Portfolio.xlsx', sheet='Drawdown')
drawdown_TQQQ_2011 <- read_excel('edit_TQQQ_2011_Portfolio.xlsx', sheet='Drawdown')
drawdown_SPY_2000 <- read_excel('edit_SPY_2000_Portfolio.xlsx', sheet='Drawdown')

table1 <- annual_QQQ_2000 %>%
  head(3) %>%
  select(Year, Return, Balance) %>%
  gridExtra::tableGrob()

table2 <- monthly_QQQ_2000 %>%
  select(Year, Month, `Portfolio 1 Return`, Balance) %>%
  head(3) %>%
  gridExtra::tableGrob()

table3 <- crash_QQQ_2000 %>%
  head(3) %>%
  gridExtra::tableGrob()

table4 <- drawdown_QQQ_2000 %>%
  head(3) %>%
  gridExtra::tableGrob()

plot_grid(table1, table2, table3, table4, labels = NULL, ncol = 1)

#str(annual_QQQ_2000)
```

**Testing Settings**

Starting balance for the test is $1200. The money inflow is $100 a month.

***Question Raised***

**1. Which is better? QQQ or TQQQ, from 2011 to 2021**

TQQQ started trading Oct 2010, so using the data from 2011.

**2. Which is better? QQQ or SPY from 2000 to 2021**


**3. Evaulate the performance and stability in the historical crash**

Dot com crash - Mar 2000 - Oct 2002

Subprime Crisis - Nov 2007 - Mar 2009

Covid-19 - Jan 2020 - Mar 2020


***1. Which is better? QQQ or TQQQ, from 2011 to 2021***

```{r}
library(dplyr)
library(tidyr)
library(ggplot2)

joined_QQQ_TQQQ <- annual_QQQ_2011 %>%
  left_join(annual_TQQQ_2011, by = c("Year" = "Year"))

plt1 <- joined_QQQ_TQQQ %>% 
  ggplot(aes(x=Year)) +
    geom_line(aes(y=Balance.x,colour = "QQQ")) + 
    geom_line(aes(y=Balance.y,colour = "TQQQ")) +
    geom_point(aes(y=Balance.x,colour = "QQQ")) +
    geom_point(aes(y=Balance.y,colour = "TQQQ")) +
    theme(axis.text.x = element_text(angle = 90, vjust = 0.5)) +
    scale_x_continuous(breaks = joined_QQQ_TQQQ$Year, labels = as.character(joined_QQQ_TQQQ$Year)) +
    scale_y_continuous(labels=scales::dollar_format()) +
    labs(title = "QQQ vs TQQQ", y="Balance")

monthly_joined_QQQ_TQQQ <- monthly_QQQ_2011 %>%
  left_join(monthly_TQQQ_2011, by = c("Year" = "Year", "Month" = "Month")) %>%
  mutate(
    Date = as.Date(paste(Year, Month, "01", sep = "-"))
  ) 

plt2 <- monthly_joined_QQQ_TQQQ %>% 
  ggplot(aes(x=Date)) +
    geom_line(aes(y=Balance.x,colour = "QQQ")) + 
    geom_line(aes(y=Balance.y,colour = "TQQQ")) +
    theme(axis.text.x = element_text(angle = 90, vjust = 0.5)) +
    scale_x_date(date_breaks = "1 year", date_labels =  "%Y") +
    scale_y_continuous(labels=scales::dollar_format()) +
    labs(title = "Monthly QQQ vs TQQQ", y="Balance")


#show(plt1)
show(plt2)

```

***QQQ vs TQQQ from 2011 to 2021***

**Total Money put**

Each $15300

**Result**

QQQ: $60,654 ($48,065 adj.)

TQQQ: $520,909 ($412,787 adj.)

**Max Drawdown**

In Covid-19 crisis

QQQ: -16.96%

TQQQ: -49.12%


***2. Which is better? QQQ or SPY from 2000 to 2021***

```{r}
library(dplyr)
library(tidyr)
library(ggplot2)

joined_QQQ_SPY <- annual_QQQ_2000 %>%
  left_join(annual_SPY_2000, by = c("Year" = "Year"))

plt1 <- joined_QQQ_SPY %>% 
  ggplot(aes(x=Year)) +
    geom_line(aes(y=Balance.x,colour = "QQQ")) + 
    geom_line(aes(y=Balance.y,colour = "SPY")) +
    geom_point(aes(y=Balance.x,colour = "QQQ")) +
    geom_point(aes(y=Balance.y,colour = "SPY")) +
    theme(axis.text.x = element_text(angle = 90, vjust = 0.5)) +
    scale_x_continuous(breaks = joined_QQQ_SPY$Year, labels = as.character(joined_QQQ_SPY$Year)) +
    scale_y_continuous(labels=scales::dollar_format()) +
    labs(title = "QQQ vs SPY", y="Balance")

monthly_joined_QQQ_SPY <- monthly_QQQ_2000 %>%
  left_join(monthly_SPY_2000, by = c("Year" = "Year", "Month" = "Month")) %>%
  mutate(
    Date = as.Date(paste(Year, Month, "01", sep = "-"))
  ) 

plt2 <- monthly_joined_QQQ_SPY %>% 
  ggplot(aes(x=Date)) +
    geom_line(aes(y=Balance.x,colour = "QQQ")) + 
    geom_line(aes(y=Balance.y,colour = "SPY")) +
    theme(axis.text.x = element_text(angle = 90, vjust = 0.5)) +
    scale_x_date(date_breaks = "1 year", date_labels =  "%Y") +
    scale_y_continuous(labels=scales::dollar_format()) +
    labs(title = "Monthly QQQ vs SPY", y="Balance")

#show(plt1)
show(plt2)

```


***QQQ vs SPY from 2000 to 2021***

**Total Money put**

Each $27500

**Result**

QQQ: $208,863 ($127,090 adj.)

SPY: $113,415 ($69,011 adj.)

**Max Drawdown**

QQQ: -81.08% Dotcom Crash

SPY: -50.80% Subprime Crisis


***3. Evaulate the performance and stability in the historical crash***

```{r}
library(dplyr)
library(tidyr)
library(ggplot2)
library(cowplot)


plt1 <- monthly_joined_QQQ_SPY %>%
  filter(Date > as.Date('2000-01-01') & Date < as.Date('2002-12-01')) %>%
  ggplot(aes(x=Date)) +
    geom_line(aes(y=Balance.x,colour = "QQQ")) + 
    geom_line(aes(y=Balance.y,colour = "SPY")) +
    theme(axis.text.x = element_text(angle = 90, vjust = 0.5)) +
    #scale_x_date(date_breaks = "1 month", date_labels =  "%m-%Y") +
    scale_y_continuous(labels=scales::dollar_format()) +
    labs(title = "Dotcom Crash QQQ vs SPY", y="Balance")

plt2 <- monthly_joined_QQQ_SPY %>%
  filter(Date > as.Date('2007-06-01') & Date < as.Date('2009-08-01')) %>%
  ggplot(aes(x=Date)) +
    geom_line(aes(y=Balance.x,colour = "QQQ")) + 
    geom_line(aes(y=Balance.y,colour = "SPY")) +
    theme(axis.text.x = element_text(angle = 90, vjust = 0.5)) +
    #scale_x_date(date_breaks = "1 month", date_labels =  "%m-%Y") +
    scale_x_date(date_breaks = "1 year", date_labels =  "%Y") +
    scale_y_continuous(labels=scales::dollar_format()) +
    labs(title = "Subprime Crisis QQQ vs SPY", y="Balance")

plt3 <- monthly_joined_QQQ_SPY %>%
  filter(Date > as.Date('2019-09-01') & Date < as.Date('2020-08-01')) %>%
  ggplot(aes(x=Date)) +
    geom_line(aes(y=Balance.x,colour = "QQQ")) + 
    geom_line(aes(y=Balance.y,colour = "SPY")) +
    theme(axis.text.x = element_text(angle = 90, vjust = 0.5)) +
    #scale_x_date(date_breaks = "1 month", date_labels =  "%m-%Y") +
    scale_x_date(date_breaks = "1 year", date_labels =  "%Y") +
    scale_y_continuous(labels=scales::dollar_format()) +
    labs(title = "Covid-19 QQQ vs SPY", y="Balance")

#plot_grid(plt1, plt2, plt3, labels = "AUTO", ncols = 2)

#show(plt1)
#show(plt2)
#show(plt3)
```


```{r}
library(dplyr)
library(tidyr)
library(ggplot2)

edit_crash_QQQ_2000 <- crash_QQQ_2000 %>% 
  select(`Stress Period`, `Portfolio 1`) %>%
  mutate(
    Ticker = "QQQ",
    Value = `Portfolio 1`*100
  )

edit_crash_SPY_2000 <- crash_SPY_2000 %>% 
  select(`Stress Period`, `Portfolio 1`) %>%
  mutate(
    Ticker = "SPY",
    Value = `Portfolio 1`*100
  )

#joined_crash_QQQ_SPY <- edit_crash_QQQ_2000 %>%
#  left_join(edit_crash_SPY_2000, by = c("Stress Period" = "Stress Period"))

added_crash_QQQ_SPY <- rbind(edit_crash_QQQ_2000, edit_crash_SPY_2000)


plt4 <- added_crash_QQQ_SPY %>% 
    group_by(`Stress Period`) %>%
    ggplot(aes(x=`Stress Period`, y = Value, fill = Ticker)) + 
    geom_bar(position = "dodge", stat = "identity") +
    theme(axis.text.x = element_text(angle = 45, vjust = 0.5))
#show(plt1)

plot_grid(plt4, plt1, plt2, plt3, labels = "AUTO", ncol = 2)

```

***Analysis in the Crash***

Because of its difference in portfolio, QQQ is more likely to have more profit, however, in Dotcom crash, due to its specialty in IT companies, it yielded lower profit than SPY.
If TQQQ existed in 2000, it would have been delisted because it will take -240% hit.
For Subprime Mortgage Crisis, Both collapsed but QQQ bounced back faster.
For Covid, Both bounced back fast.

***Conclusion***

TQQQ: $15,300 -> $520,909 (3404%)

QQQ (from 2011): $15,300 -> $60,654 (396%)

QQQ (from 2000): $27,500 -> $208,863 (759%)

SPY: $27,500 -> $113,415 (412%)

Significant increase in balance for all four test results, but TQQQ is the best in terms of profit. However, one should think about extreme case like Dotcom crash if they intend to invest in TQQQ. 
SPY has the lowest profit after all but had the best stability overall.

It is solely on your decision which index ETF to buy, but it is very important to think about drawdown when investing on the leveraged ETFs such as TQQQ. As I mentioned multiple times, if Dotcom crash equivalent event happend after 2010, TQQQ would have been delisted from NASDAQ and people invested in the TQQQ will take -100% loss in their money.

Not only profit, but also stability is the important factor to think about to invest your money. So please take consideration of your own and proceed with confidence.

***Happy investing!***
