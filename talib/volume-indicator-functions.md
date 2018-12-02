# Volume Indicator Functions

## AD - Chaikin A/D Line 

TODO\(not finish reading yet\)

### Introduction <a id="introduction"></a>

Developed by Marc Chaikin, the Chaikin Oscillator measures the momentum of the Accumulation Distribution Line using the [MACD formula](https://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:moving_average_convergence_divergence_macd). This makes it an indicator of an indicator. The Chaikin Oscillator is the difference between the 3-day EMA of the Accumulation Distribution Line and the 10-day EMA of the Accumulation Distribution Line. Like other momentum indicators, this indicator is designed to anticipate directional changes in the Accumulation Distribution Line by measuring the momentum behind the movements. A momentum change is the first step to a trend change. Anticipating trend changes in the Accumulation Distribution Line can help chartists anticipate trend changes in the underlying security. The Chaikin Oscillator generates signals with crosses above/below the zero line or with bullish/bearish divergences.

### Calculation <a id="calculation"></a>

Calculating the Accumulation Distribution Line \(ADL\) is the first step to the Chaikin Oscillator. This article will cover the basic elements of the Accumulation Distribution Line. See our [ChartSchool article](https://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:accumulation_distribution_line) the details. There are three steps to calculating the Accumulation Distribution Line \(ADL\). First, calculate the Money Flow Multiplier. Second, multiply this value by volume to find Money Flow Volume. Third, create a running total of Money Flow Volume to form the Accumulation Distribution Line \(ADL\). Fourth, take the difference between two moving averages to calculate the Chaikin Oscillator.

```text
               
  1. Money Flow Multiplier = [(Close  -  Low) - (High - Close)] /(High - Low) 

  2. Money Flow Volume = Money Flow Multiplier x Volume for the Period

  3. ADL = Previous ADL + Current Period's Money Flow Volume

  4. Chaikin Oscillator = (3-day EMA of ADL)  -  (10-day EMA of ADL)		
```

The Accumulation Distribution Line rises when the Money Flow Multiplier is positive and falls when negative. This multiplier is positive when the close is in the upper a half of the period's high-low range and negative when the close is in the lower half. As a MACD type oscillator, the Chaikin Oscillator turns positive when the faster 3-day EMA moves above the slower 10-day EMA. Conversely, the indicator turns negative when the 3-day EMA moves below the 10-day EMA.

![Chart 1  -  Chaikin Oscillator](https://d.stockcharts.com/school/data/media/chart_school/technical_indicators_and_overlays/chaikin_oscillator/chosc-1-geexam.png)

The chart above shows the Accumulation Distribution Line \(gray\) with the 3-day EMA in \(blue\) and the 10-day EMA \(red\). The price for General Electric \(GE\) is invisible so we can focus on the relationship between the Accumulation Distribution Line and the Chaikin Oscillator. Notice how the Chaikin Oscillator moves into negative territory as the 3-day EMA moves below the 10-day EMA. Conversely, the oscillator turns positive when the 3-day EMA crosses above the 10-day EMA.

### Interpretation <a id="interpretation"></a>

First and foremost, it is important to remember that the Chaikin Oscillator is an indicator of an indicator. It measures momentum for the Accumulation Distribution Line. This makes it at least three steps removed from the price of the underlying security. First, price and volume are reshaped into the Accumulation Distribution Line. Second, exponential moving averages are applied to the Accumulation Distribution Line. Third, the difference between the [moving averages](https://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:moving_averages) is used to form the Chaikin Oscillator. As the third derivative, the indicator is more prone to disconnect from the price of the underlying security.

![Chart 2  -  Chaikin Oscillator](https://d.stockcharts.com/school/data/media/chart_school/technical_indicators_and_overlays/chaikin_oscillator/chosc-2-msftderiv.png)

Having clarified that, the indicator is designed to measure the momentum behind buying and selling pressure \(Accumulation Distribution Line\). A move into positive territory indicates that the Accumulation Distribution Line is rising and buying pressure prevails. A move into negative territory indicates that the Accumulation Distribution Line is falling and selling pressure prevails. Chartists can anticipate crosses into positive or negative territory by looking for bullish or bearish divergences, respectively.

### Buying/Selling Bias <a id="buying_selling_bias"></a>

The Chaikin oscillator can be used to define a general buying or selling bias simply with positive or negative values. The indicator oscillates above/below the zero line. Generally, buying pressure is stronger when the indicator is positive and selling pressure is stronger when the indicator is negative.

The default settings for the Chaikin Oscillator \(3,10\) often produce a line that frequently crosses zero. Chartists can smooth the indicator by lengthening the moving averages. The example below shows the Chaikin Oscillator \(6,20\). Both moving averages were doubled to maintain the ratio and smooth the indicator.

![Chart 3  -  Chaikin Oscillator](https://d.stockcharts.com/school/data/media/chart_school/technical_indicators_and_overlays/chaikin_oscillator/chosc-3-xcross.png)

The Chaikin Oscillator for US Steel \(X\) crossed the zero line six times over 12 months. There were some good signals, such as the April sell signal and the October buy signal. There were also some bad signals or whipsaws. The key, as with all indicators, is to confirm the oscillator signals with other aspects of technical analysis, such as a pure price momentum oscillator or pattern analysis.

![Chart 4  -  Chaikin Oscillator](https://d.stockcharts.com/school/data/media/chart_school/technical_indicators_and_overlays/chaikin_oscillator/chosc-4-aacross.png)

The chart for Alcoa \(AA\) shows six zero-line crosses in 2010. The first five did not generate good signals, but the sixth was a dandy. Chartists should experiment with the settings and consider adding trend lines to enhance their analysis. Trend line breaks are often earlier than zero line crosses. A trend line also captures the direction of the indicator. A rising Chaikin Oscillator reflects a steady increase in buying pressure. A falling Chaikin Oscillator reflects a steady increase in selling pressure.

### Divergences <a id="divergences"></a>

Bullish and bearish divergences alert chartists to a momentum shift in buying or selling pressure that can foreshadow a trend reversal on the price chart. A bullish divergence forms when price moves to new lows and the Chaikin Oscillator forms a higher low. This higher low shows less selling pressure. It is important to wait for some sort of confirmation, such as an upturn in the indicator or a cross into positive territory. A move into positive territory shows upside momentum in the Accumulation Distribution Line.

The Fastenal \(FAST\) chart shows five divergences for the Chaikin Oscillator in 2010. The default settings \(3,10\) produce a rather sensitive oscillator that will generate many divergences. The key is to differentiate the robust signals from the bogus signals by waiting for confirmation. Even with a bullish divergence, selling pressure outweighs buying pressure until there is a cross above the zero line. Buying pressure dominates until there is a cross into negative territory.

![Chart 5  -  Chaikin Oscillator](https://d.stockcharts.com/school/data/media/chart_school/technical_indicators_and_overlays/chaikin_oscillator/chosc-5-fastbudd.png)

The green lines show the Chaikin Oscillator forming a higher low as the stock forms a lower low for a bullish divergence. The green dotted lines show when the indicator moves into positive territory to confirm the signal. The mid-February, early September and late November signals were great. The mid-June buy signal would have resulted in a whipsaw and there was not much weakness after the October sell signal from the bearish divergence.

A bearish divergence forms when price moves to a new high and the Chaikin Oscillator fails to confirm this higher high. This failure reflects less buying pressure that can sometimes foreshadow a bearish reversal on the price chart. Confirmation comes when the oscillator moves into negative territory.

![Chart 6  -  Chaikin Oscillator ](https://d.stockcharts.com/school/data/media/chart_school/technical_indicators_and_overlays/chaikin_oscillator/chosc-6-kssbedd.png)

The chart for Kohls \(KSS\) shows three bearish divergences and two bullish divergences over a 12 month period. The bearish divergences \(red lines\) were confirmed when the Chaikin Oscillator moved into negative territory to show actual downside momentum in the Accumulation Distribution Line. Remember, the Chaikin Oscillator \(3,10\) turns negative when the 3-day EMA of the Accumulation Distribution Line moves below the 10-day EMA.

### Conclusions <a id="conclusions"></a>

The Chaikin Oscillator is a momentum indicator for the Accumulation Distribution Line. Basically, the Chaikin Oscillator turbo charges the Accumulation Distribution Line by measuring momentum. Signals are more frequent and often easier to quantify using the Chaikin Oscillator. As a money flow oscillator it can be used in conjunction with pure price oscillators, such as MACD or [RSI](https://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:relative_strength_index_rsi). As with all indicators, the Chaikin Oscillator should not be used as a stand-alone indicator.

### Using with SharpCharts <a id="using_with_sharpcharts"></a>

The Chaikin Oscillator can be set as an indicator above, below or behind a security's price plot. It is easy to compare indicator/price movements when the indicator is placed behind the price plot. Once the indicator is chosen from the dropdown list, the default parameter setting appears \(3,10\). These parameters can be adjusted to increase or decrease sensitivity. Users can click on “advanced options” to add a horizontal line or moving average. [Click here for a live example](http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=6&dy=0&id=p43640188268&listNum=30&a=222998125).

![Chart 7  -  Chaikin Oscillator](https://d.stockcharts.com/school/data/media/chart_school/technical_indicators_and_overlays/chaikin_oscillator/chosc-7-ibmlive.png)

![SharpCharts  -  Chaikin Oscillator](https://d.stockcharts.com/school/data/media/chart_school/technical_indicators_and_overlays/chaikin_oscillator/chosc-8-shch.png)

### Suggested Scans <a id="suggested_scans"></a>

#### Chaikin Oscillator Turns Positive and RSI Moves Above 55 <a id="chaikin_oscillator_turns_positive_and_rsi_moves_above_55"></a>

This scan starts with a base of stocks that are averaging at least $10 in price and 100,000 in daily volume over the last 60 days. Upturns on good volume are identified when the Chaikin Oscillator moves above +1000, which is just above its centerline \(0\). This is confirmed with price momentum because RSI is required to move above 55, which is just above its centerline \(50\). This scan is meant as a starting point for further analysis and due diligence.

```text
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily Chaikin Osc(3,10) crosses 1000] 
AND [Daily RSI(14,Daily Close) crosses 55]
```

#### Chaikin Oscillator Turns Negative and RSI Moves Below 45 <a id="chaikin_oscillator_turns_negative_and_rsi_moves_below_45"></a>

This scan starts with a base of stocks that are averaging at least $10 in price and 100,000 in daily volume over the last 60 days. Downturns on good volume are identified when the Chaikin Oscillator moves below -1000, which is just below its centerline \(0\). This is confirmed with price momentum because RSI is required to move below 45, which is just below its centerline \(50\). This scan is meant as a starting point for further analysis and due diligence.

```text
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [-1000 crosses Daily Chaikin Osc(3,10)] 
AND [45 crosses Daily RSI(14,Daily Close)]
```

For more details on the syntax to use for Chaikin Oscillator scans, please see our [Scanning Indicator Reference](http://stockcharts.com/docs/doku.php?id=scans:indicators#chaikin_oscillator_chaikin_osc) in the Support Center.

### Further Study <a id="further_study"></a>

This book covers it all with explanations that are simple and clear. Murphy covers most the major charts patterns and indicators. A complete chapter is devoted to understanding volume and open interest.

{% embed url="https://stockcharts.com/school/doku.php?id=chart\_school:technical\_indicators:chaikin\_oscillator" %}



{% embed url="https://mrjbq7.github.io/ta-lib/func\_groups/volume\_indicators.html" %}

