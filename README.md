# Pairs-Trading-Analyzer
<p style="text-align: center;">C# Console Application:
Asks for two files containing historical financial data in the same format as files from Yahoo Finance. Performs the two-step Engel-Granger Test for Cointegration and simulates profits of applying the Pairs Trading Strategy to these stocks. To Project further Includes code to conduct statistical inference and a Function to perform the Augmented Dickey Fuller Test for stationarity of a timeseries, which is part of the Engel-Granger Test for cointegration.</p>


## How to use it:
<p style="text-align: center;">Clone the repository with Visual Studio to a local directory on your machine. Open the Program.cs file. Ensure in the Nuget Manager that the package Math.Numerics is available. Run/ Debug the application.
When propted, copy paste paths referencing to the historical price data for the two stocks. According data can be downloaded from Yahoo finance.
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

<p style="text-align: center;">Later versions of this program might facilitate the analysis of multiple stocks, repeated trade simulations with different parameters and an inmproved treatment of the problem of heteroskedasticly distributed deviations by improving the estimator of the relative valuation. For instance, replacing the moving average model, with an SARIMA model of the relative valuation. A better fitting model, that that yields more "up todate" estimates of the average value should not suffer as strongly from trends in the relative valuation and possibly also reduce the effect ofskewed deviations in the relative valuation of the stocks.</p>

## How to choose pairs for Testing
