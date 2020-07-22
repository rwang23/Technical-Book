#TD and Chan in tradingview


##Algorithm


##How to use
* Same as TTMSqueeze, please click left and select TTMSqueeze

##PineScript Code

```
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © rwang23

study("TDChan",overlay=true)
transp=input(0)
Numbers=input(true)
SR=input(true)
Barcolor=input(true)
TD = close > close[4] ?nz(TD[1])+1:0
TS = close < close[4] ?nz(TS[1])+1:0

difen1 = high[2] > high[1] and low[2] > low[1] and high[1] < high and low[1] < low
dingfen1 = high[2] < high[1] and low[2] < low[1] and high[1] > high and low[1] > low
difen2 = low[1] < low[2] and low[1] < low[3] and low[1] < low[4] and low[1] < low[5] and low[1] < low[6] and low[1] < low[7]
dingfen2 = high[1] > high[2] and high[1] > high[3] and high[1] > high[4] and high[1] > high[5] and high[1] > high[6] and high[1] > high[7]
difen = difen1 and difen2
dingfen = dingfen1 and dingfen2

TDUp = TD - valuewhen(TD < TD[1], TD , 1 )
TDDn = TS - valuewhen(TS < TS[1], TS , 1 )
//plotshape(Numbers?(TDUp==1?true:na):na,style=shape.triangledown,text="1",color=green,location=location.abovebar,transp=transp)
//plotshape(Numbers?(TDUp==2?true:na):na,style=shape.triangledown,text="2",color=green,location=location.abovebar,transp=transp)
//plotshape(Numbers?(TDUp==3?true:na):na,style=shape.triangledown,text="3",color=green,location=location.abovebar,transp=transp)
//plotshape(Numbers?(TDUp==4?true:na):na,style=shape.triangledown,text="4",color=green,location=location.abovebar,transp=transp)
//plotshape(Numbers?(TDUp==5?true:na):na,style=shape.triangledown,text="5",color=green,location=location.abovebar,transp=transp)
//plotshape(Numbers?(TDUp==6?true:na):na,style=shape.triangledown,text="6",color=green,location=location.abovebar,transp=transp)
plotshape(Numbers?(TDUp==7?true:na):na,style=shape.triangledown,text="7",color=green,location=location.abovebar,transp=transp)
plotshape(Numbers?(TDUp==8?true:na):na,style=shape.triangledown,text="8",color=green,location=location.abovebar,transp=transp)
plotshape(Numbers?(TDUp==9?true:na):na,style=shape.triangledown,text="9",color=green,location=location.abovebar,transp=transp)

//plotshape(Numbers?(TDDn==1?true:na):na,style=shape.triangleup,text="1",color=red,location=location.belowbar,transp=transp)
//plotshape(Numbers?(TDDn==2?true:na):na,style=shape.triangleup,text="2",color=red,location=location.belowbar,transp=transp)
//plotshape(Numbers?(TDDn==3?true:na):na,style=shape.triangleup,text="3",color=red,location=location.belowbar,transp=transp)
//plotshape(Numbers?(TDDn==4?true:na):na,style=shape.triangleup,text="4",color=red,location=location.belowbar,transp=transp)
//plotshape(Numbers?(TDDn==5?true:na):na,style=shape.triangleup,text="5",color=red,location=location.belowbar,transp=transp)
//plotshape(Numbers?(TDDn==6?true:na):na,style=shape.triangleup,text="6",color=red,location=location.belowbar,transp=transp)
plotshape(Numbers?(TDDn==7?true:na):na,style=shape.triangleup,text="7",color=red,location=location.belowbar,transp=transp)
plotshape(Numbers?(TDDn==8?true:na):na,style=shape.triangleup,text="8",color=red,location=location.belowbar,transp=transp)
plotshape(Numbers?(TDDn==9?true:na):na,style=shape.triangleup,text="9",color=red,location=location.belowbar,transp=transp)

plotshape(difen,style=shape.xcross,text="+",color=green,location=location.belowbar,transp=transp,offset=-1)
plotshape(dingfen,style=shape.xcross,text="-",color=red,location=location.abovebar,transp=transp,offset=-1)


// Sell Setup //
//------------//
priceflip = barssince(close<close[4])
sellsetup = close>close[4] and priceflip
sell = sellsetup and barssince(priceflip!=9)
sellovershoot = sellsetup and barssince(priceflip!=13)
sellovershoot1 = sellsetup and barssince(priceflip!=14)
sellovershoot2 = sellsetup and barssince(priceflip!=15)
sellovershoot3 = sellsetup and barssince(priceflip!=16)

//----------//
// Buy setup//
//----------//
priceflip1 = barssince(close>close[4])
buysetup = close<close[4] and priceflip1
buy = buysetup and barssince(priceflip1!=9)
buyovershoot = barssince(priceflip1!=13) and buysetup
buyovershoot1 = barssince(priceflip1!=14) and buysetup
buyovershoot2 = barssince(priceflip1!=15) and buysetup
buyovershoot3 = barssince(priceflip1!=16) and buysetup

//----------//
// TD lines //
//----------//
TDbuyh = valuewhen(buy,high,0)
TDbuyl = valuewhen(buy,low,0)
TDsellh = valuewhen(sell,high,0)
TDselll = valuewhen(sell,low,0)

//----------//
//   Plots  //
//----------//

//plot(SR?(TDbuyh ? TDbuyl: na):na,style=circles, linewidth=1, color=red)
//plot(SR?(TDselll ? TDsellh : na):na,style=circles, linewidth=1, color=lime)
barcolor(Barcolor?(sell? #FF4DFB : buy? #33FF57 : sellovershoot? #FF66A3 : sellovershoot1? #FF3385 : sellovershoot2? #FF0066 : sellovershoot3? #CC0052 : buyovershoot? #D6FF5C : buyovershoot1? #D1FF47 : buyovershoot2? #B8E62E : buyovershoot3? #8FB224 : na):na)


```
