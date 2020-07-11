#TTM Squeeze in tradingview


##Algorithm
View [TTM Squeeze Algorithm](https://www.cypherscope.com/home/the-best-indicators-youve-never-used-ttm-squeeze#:~:text=The%20TTM%20Squeeze%20captures%20the,subsequent%20direction%20of%20that%20move) to view how TTM Squeeze works


##PineScript Code

```
//@version=4
study("TTM Squeeze", shorttitle="My TTM Squeeze")

length = input(title="Length", type=input.integer, defval=20)
bbMult = input(title="Bollinger Bands Multiplier", type=input.float, step=0.1, defval=2.0)
kcMult = input(title="Keltner Channels Multiplier", type=input.float, step=0.1, defval=1.5)


smoothLength = input(title="EMA Smooth Length", type=input.integer, defval=3)
dotDisplayRatio = 1.0
src = close

//Bollinger Bands
mean = sma(src, length)
stdev = stdev(src, length)
//bbUpper = mean + bbMult * stdev
//bbLower = mean - bbMult * stdev
//BB Range
bbRange = 2 * bbMult * stdev / mean

//Keltner Channels
basis = ema(src, length)
avgrange = ema(tr(true), length)
//kcUpper = basis + kcMult * avgrange
//kcLower = basis - kcMult * avgrange
//KC range
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

dotColor = bbRange / kcRange <= dotDisplayRatio ? color.orange : #00d916
plot(0, title="Squeeze dot", style=plot.style_circles, linewidth=3, color=dotColor)

```
