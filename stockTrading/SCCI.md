// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © rwang23

//@version=4
study("CCI New Algorithm", shorttitle="My SCCI", overlay=false)

source = input(close)
cci_period = input(28, "CCI Period")
stoch_period = input(28, "Stoch Period")
stoch_smooth_k = input(3, "Stoch Smooth K")
stoch_smooth_d = input(3, "Stoch Smooth D")
d_or_k = input(defval="D", options=["D", "K"])
OB = 80
OS = 20

showArrows = input(true, "Show Arrows")
showArrowsEnter = input(true, "Show Enter ")
showArrowsCenter = input(false, "Show Center ")
showArrowsExit = input(true, "Show Exit ")

cci = cci(source, cci_period)
stoch_cci_k = sma(stoch(cci, cci, cci, stoch_period), stoch_smooth_k)
stoch_cci_d = sma(stoch_cci_k, stoch_smooth_d)

ma = (d_or_k == "D") ? stoch_cci_d : stoch_cci_k

trend_enter = if showArrowsEnter
    if crossunder(ma, OS)
        1
    else
        if crossover(ma, OB)
            -1

//use exit to  confirm enter
trend_exit = if showArrowsExit
    if crossunder(ma, OB)
        -1
    else
        if crossover(ma, OS)
            1

trend_center = if showArrowsCenter
    if crossunder(ma, 50)
        -1
    else
        if crossover(ma, 50)
            1

// plot the OB and OS level
overbought = hline(OB, linewidth=1, color=color.red)
oversold = hline(OS, linewidth=1, color=color.lime)
fill(overbought, oversold, color=color.purple, transp=95)

// Plot the moving average
ma_color = ma > OB ? color.red : ma < OS ? #00d916 : #158cd1
plot(ma, "Moving Average", linewidth=2, color=ma_color, transp=0)
maxLevelPlot = hline(100, title="Max Level", linestyle=hline.style_dotted, color=color.new(color.white, 100))
minLevelPlot = hline(0, title="Min Level", linestyle=hline.style_dotted, color=color.new(color.white, 100))
//overbought = hline(OB, title="Hline Overbought", linestyle=hline.style_solid, color=color.new(color.white, 100))
//oversold = hline(OS, title="Hline Oversold", linestyle=hline.style_solid, color=color.new(color.white, 100))

color_fill_os = ma > OB ? color.new(color.red,90) : color.new(color.white, 100)
color_fill_ob = ma < OS ? color.new(color.green,90) : color.new(color.white, 100)
fill(maxLevelPlot, overbought, color=color_fill_os)
fill(minLevelPlot, oversold, color=color_fill_ob)

// Show the arrows
// Trend Enter
plotshape((showArrows and showArrowsEnter and trend_enter == 1) ? 0 : na, color=color.green, transp=20, style=shape.arrowup, size=size.normal,  location=location.absolute, title="Trend Enter Buy")
plotshape((showArrows and showArrowsEnter and trend_enter == -1) ? 100 : na, color=color.red, transp=20, style=shape.arrowdown, size=size.normal, location=location.absolute, title="Trend Enter Sell")

// Trend Center
plotshape((showArrows and showArrowsCenter and trend_center == 1) ? 35 : na, color=color.aqua, transp=20, style=shape.arrowup, size=size.normal, location=location.absolute, title="Trend Center Buy")
plotshape((showArrows and showArrowsCenter and trend_center == -1) ? 65 : na, color=color.fuchsia, transp=20, style=shape.arrowdown, size=size.normal, location=location.absolute, title="Trend Center Sell")

// Trend Exit
plotshape((showArrows and showArrowsExit and trend_exit == 1) ? 0 : na, color=color.orange, transp=20, style=shape.arrowup, size=size.normal, location=location.absolute, title="Trend Exit Buy")
plotshape((showArrows and showArrowsExit and trend_exit == -1) ? 100 : na, color=color.maroon, transp=20, style=shape.arrowdown, size=size.normal, location=location.absolute, title="Trend Exit Sell")

alertcondition((showArrows and showArrowsEnter and trend_enter == 1), message="Trend Enter Buy", title="Trend Enter Buy")
alertcondition((showArrows and showArrowsEnter and trend_enter == -1), message="Trend Enter Sell", title="Trend Enter Sell")
alertcondition((showArrows and showArrowsCenter and trend_center == 1), message="Trend Center Buy", title="Trend Center Buy")
alertcondition((showArrows and showArrowsCenter and trend_center == -1), message="Trend Center Sell", title="Trend Center Sell")
alertcondition((showArrows and showArrowsExit and trend_exit == 1), message="Trend Exit Buy", title="Trend Exit Buy")
alertcondition((showArrows and showArrowsExit and trend_exit == -1), message="Trend Exit Sell", title="Trend Exit Sell")
