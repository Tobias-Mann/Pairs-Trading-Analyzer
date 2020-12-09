# Pairs-Trading-Analyzer
<p style="text-align: center;">C# Console Application:
Asks for two files containing historical financial data in the same format as files from Yahoo Finance. Performs the two-step Engel-Granger Test for Cointegration and simulates profits of applying the Pairs Trading Strategy to these stocks. To Project further Includes code to conduct statistical inference and a Function to perform the Augmented Dickey Fuller Test for stationarity of a timeseries, which is part of the Engel-Granger Test for cointegration.</p>

## Motivation for Trading Pairs Strategy
<p style="text-align: center;">Generally stock pairs that might be strongly affected by the same economic conditions tend to perform well under this strategy. However, in theory any valuation relevant similarity between stocks could be used to apply the strategy, like similar structure of the balance sheet. The idea is to identify short term deviations from a long term relative valuation and try to arbitrage these deviations, by shorting the overvalued stock and at the same time going long on the undervalued stock. A nice side effect of this strategy is that at any given time, the portfolio is Hedged against market shocks, as there is always an equally balanced exposure to a short position. However, the simulation ignores any costs that would theoretically apply, such as interest on the borrowed stock for the short position, transaction cost and comissions and in the case of large trades, liquidity constrained gains. Insted the simulation assumes,that always the colsing price of the  next day can be realized. However, using limit orders the so calculated returns could likely be outperformed!</p>

## Ideas for pairs to analyze:
- American Prison stocks: GEO & CXW
- Swiss Pharmaceutical Giants: Hoffmann-La Roche & Novartis
- German Car Manufacturers: Daimler & Porsche
- Investment Banks: Citi & J.P. Morgan

## How to use the Program
<p style="text-align: center;">Clone the repository to a local directory on your machine. Open the Program.cs file with Visual Studio. Ensure in the Nuget Manager that the package Math.Numerics is available. Otherwise, install/restore, the Nuget and run/build or debug the application.
When the console asks for the files, copy/paste the paths referencing to the historical price data. According data can be downloaded from Yahoo finance.
Any Data used must be a csv (comma seperated not by semicolon), that contains a date parseble in the first column and the closing price in the fith colum.</p>

![](https://github.com/Tobias-Mann/Pairs-Trading-Analyzer/blob/master/Screenshots/Inputs.png?raw=true)

<p> The csv files in Excel:</p>

![](https://github.com/Tobias-Mann/Pairs-Trading-Analyzer/blob/master/Screenshots/Data%20In%20Excel.png?raw=true)

## How to interpret the output
<p style="text-align: center;">First, the program analyzes the two stocks for possible cointegration using the two step Engel-Granger approach (described further below).
This indicates how profitable a pairs trading Strategy might be. The screenshot below shows what an example output of the analysis for the stock pair Novartis and Roche</p>

![](https://github.com/Tobias-Mann/Pairs-Trading-Analyzer/blob/master/Screenshots/Cointegration%20Analysis.png?raw=true)

<p>Secondly, returns of a pairs trading strategy are simulated, by default the simulation uses a 50-day moving average. Parameters in the code can be changed to simulate different moving averages or to replace the average with a static average, based on the entire sample. The latter is not recommendable as trading results might be significantly distorted. Depending on what stock is assigned first, the strategies returns are drastically different. The smoothing average yields more consistent results. However, retruns may still vary depending on the order in which the stocks are feeded into the program. This is due to the Heteroskedastic deviations in the relative valuations of two stocks. In other words, the strategy behaves as if, the stocks have a constant (or moving) relative valuation, where any deviations in the deviation are normally distributed around the estimated mean. However, in reality these deviations might be heavily skewed or auto-correllated, both causes the strategy to yield inconsistent returns depending on the order of inputs, as this deterines enumerator and denominator of the relative valuation.</p> <p>The Screenshot below Illustrates the simulation Output for the stock pair Novartis and Roche</p>

![](https://github.com/Tobias-Mann/Pairs-Trading-Analyzer/blob/master/Screenshots/Simulation%20of%20Trades.png?raw=true)

## Outlook
<p style="text-align: center;">Later versions of this program might facilitate the analysis of multiple stocks, repeated trade simulations with different parameters and an inmproved treatment of the problem of heteroskedasticly distributed deviations by improving the estimator of the relative valuation. For instance, replacing the moving average model, with an SARIMA model of the relative valuation. A better fitting model, that that yields more "up todate" estimates of the average value should not suffer as strongly from trends in the relative valuation and possibly also reduce the effect ofskewed deviations in the relative valuation of the stocks.</p>
