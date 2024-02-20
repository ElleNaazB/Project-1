

# Introduction 


This project conducts a thorough analysis of the stock performance of the top 5 companies in the S&P 500 index: Apple Inc., Microsoft Corp., Amazon.com Inc., NVIDIA Corp., and Alphabet Inc. Class A. By integrating both fundamental and technical analysis, we aim to enhance investment decision-making. Through fundamental analysis, the project focuses on assessing the financial health of these companies by examining their overall financial condition and identifying potential risk, which informs the long-term investment potential.Concurrently, technical analysis is used to analyze stock price trends,cumulative return, volatility, and comparative performance, as well as identify correlations and significant long-term trends in their trading data. Our analysis culminates in a recommendation of what we believe to be the best investment opportunity among these top performers. Our aim is to provide a complete picture of the financial stability and growth potential of these industry giants, thus empowering investors with the knowledge needed to make well-informed investment choices.

# Methodology 
## Installation
For this project, we used  datasets from the yahoo finance library in python. 
The library could be installed by the command: 
```{r import-data, echo = TRUE}
$ pip install yfinance --upgrade --no-cache-dir
```
## Download Historical Data Using the Yahoo Finance API
```{r import-data, echo = TRUE}
from yahoo_fin.stock_info import get_data
```
## Import Data
For example:
```{r import-data, echo = TRUE}
import yfinance as yf
msft = yf.Ticker("MSFT")
print(msft.info)
```
## Methods used for Exploratory Data Analysis
The project uses a decade's worth of data, spanning from 2013 to 2023, to conduct a thorough Exploratory Data Analysis (EDA). This comprehensive approach allows us to understand the dataset, aiming to uncover underlying patterns, trends, and anomalies within the stock performances of our subjects. 

### Moving Averages and Correlation Matrix
Moving averages with rolling windows of 50 and 200 days has been used to assess the underlying trends in stock prices. This approach is used to smooth out short-term fluctuations and highlight longer-term movements, facilitating a clearer understanding of directional momentum within the market. 
Investigated the potential correlations between the opening prices of these companies, we constructed a correlation matrix. This matrix is used to quantitatively measure the degree to which the stock prices of these entities move in relation to one another, providing insights into potential co-movements or divergences in their stock price behaviors.
## Analysis 

### Volatility: 
The findings indicated that Nvidia (NVDA) has the highest volatility among the five stocks. Its stock price has been the most prone to large swings. This suggests that Nvidia's stock has been the most unpredictable and may be considered the riskiest investment of the five .


### Financial Analysis

#### Price Earning Ratio and Risk

From the generated price earning ratio graph from yfinance data, company NVIDIA flagging high of 96.18 and shows highest future growth whereas Google stock seems to be undervalued as it remains low at 24.23. Company Amazon reflects with the second highest price earning score of 58.45.

Looking at the risk radar plot, NVIDIA shows highest risk of 1.68 showing most volatility among the 5 companies compared. In contrast Microsoft shows 0.9 beta value (<1) showing more stability in the stock market value.

<img src="https://github.com/ElleNaazB/Project-1/blob/Santosh/IMAGE1.png">  <img src= "https://github.com/ElleNaazB/Project-1/blob/Santosh/IMAGE2.png">

#### Revenue VS Profit Margin

From the comparison of the following graphs, it is noted that Amazon is generating the highest revenue of 575 billion whereas profit margin remains low. We noted is due to competitive pricing strategies or new investments strategies.

Even if, NVDA has the lowest revenue across 5 companies, it is showing the highest profit margin of on or above 0.40. When further explored it was noted tech giants including Google, Meta and others are massively using NVIDIA produced chips to drive their AI technologies.

With the 307 billions of total revenue, Google was able to gain approximately 0.20 profit margin.

<img src="https://github.com/ElleNaazB/Project-1/blob/Santosh/IMAGE3.png"> <img src="https://github.com/ElleNaazB/Project-1/blob/Santosh/IMAGE4.png">

####  Market Capitalization, Price Earning and Earning Per Share

While reviewing the following combined graph, it is noted that Microsoft remains at the top securing highest market capitalization with 3002.34 billion shares and also remains first in demonstrating highest earning per share amount of 11.07. The second highest market coverage is captured by Apple however it’s earning per share remains low of 6.44 which just higher than Google (5.80) however below than NVDA. In contrast Amazon remained lowest in generating earning per share amount of just $2.90. Even though it’s price earning remained the highest of 58.45, the earning per share amount was significantly lower of 2.90.

<img src="https://github.com/ElleNaazB/Project-1/blob/Santosh/IMAGE%205.png">


## Limitations 
While our exploratory data analysis provides valuable insights into the stock performance of the top 5 S&P 500 companies, it is important to acknowledge certain limitations of our study. Firstly, our analysis was confined to EDA and did not incorporate technical analysis, which might have offered additional perspectives on market entry points and the timing of stock price movements. The absence of such technical insights means that our conclusions are better suited for understanding long-term trends rather than short-term trading opportunities.

Moreover, the stock market is subject to rapid fluctuations influenced by a multitude of external factors beyond a company's performance.

Our study did not also explicitly model the impact of global economic events, policy changes, or market sentiment shifts, which can all drastically alter stock performance. Future studies may benefit from incorporating a more holistic approach that includes these external variables, along with a multi-faceted analysis combining EDA, fundamental and technical analysis to provide a more comprehensive view of stock performance and investment potential.
## Conclusion
The goal of the project was to recommend of what we believe to be the best investment opportunity among these top 5 performers in S&P500. The analysis reveals that Microsoft stands out as the most stable stock, offering consistent performance with lower volatility. On the other hand, NVIDIA, despite its higher volatility, shows substantial growth potential, suggesting an attractive option for risk-tolerant investors aiming for higher returns.

