#TTM Squeeze in tradingview


##Algorithm
Click [TTM Squeeze Algorithm](https://www.cypherscope.com/home/the-best-indicators-youve-never-used-ttm-squeeze#:~:text=The%20TTM%20Squeeze%20captures%20the,subsequent%20direction%20of%20that%20move) to view how TTM Squeeze works

##How to use
* Navigate to tradingview chart
* Open Pine Editor at bottom of the page
* Click New -> Blank indicator script
* Copy code and save
* Click Indicators at top of the page -> My scripts -> choose your copy
* For futu users, please replace the functions with those supported by futu

##PineScript Code

```
//@version=4
study("TTM Squeeze", shorttitle="My TTM Squeeze")

length = input(title="Length", type=input.integer, defval=14)
bbMult = input(title="Bollinger Bands Multiplier", type=input.float, step=0.1, defval=2.0)
kcMult = input(title="Keltner Channels Multiplier", type=input.float, step=0.1, defval=1.5)

smoothLength = input(title="EMA Smooth Length", type=input.integer, defval=3)
//dotDisplayRatio = 1.0
dotAdjustatio = input(title="Dot Adjust Ratio", type=input.float, step=0.1, defval=1.1)
src = close

//Bollinger Bands
mean = sma(src, length)
stdev = stdev(src, length)
bbRange = 2 * bbMult * stdev / mean

//Keltner Channels
basis = ema(src, length)
avgrange = ema(tr(true), length)
kcRange = 2 * kcMult * avgrange / basis

//Momentum
momentum = change(src, length)

//histogram Smoothing
hist = ema(momentum, smoothLength)

col_grow_above = #26A69A
col_grow_below = #FFCDD2
col_fall_above = #B2DFDB
col_fall_below = #EF5350

histColor = hist >= 0 ? hist[1] < hist ? col_grow_above : col_fall_above : hist[1] < hist ? col_grow_below : col_fall_below
plot(hist, style=plot.style_columns, color=histColor, histbase=0)

dotColor = bbRange / kcRange <= dotAdjustatio ? color.orange : #00d916
plot(0, title="Squeeze dot", style=plot.style_circles, linewidth=4, color=dotColor)

```
