/*
M_Prompt.trl
build indicators for ChatGPT

*/
tick: symbol=@ES5m,bar=700
rule: setup
 c=Close()
 price=Close()
 vp=VWAP()
 ema9=EMA(9)
 ema21=EMA(21)
 ema50=EMA(50)
 vwap=vp.getVwap()
 rsi14=RSI(14)
 stoch14=Stoch(14,3)
 atr14=ATR(14)
 vol=Volume()
 avgVol=AvgVolume(14)
 plot line,vwap
 plot 1,line,rsi14
 plot 1,line,[30,50,70]

after: save results
  o=Prompt("price,ema9,ema21,ema50,vwap,rsi14,stoch14,atr14,vol,avgVol")
  plot mix,o.getMix()
  o.printBigBarData("C:/projects/menus/kodatrades/data/data5m.csv", 1, 40)
  o.printBigBarData("C:/projects/menus/kodatrades/data/data15m.csv", 3, 40)
  o.printBigBarData("C:/projects/menus/kodatrades/data/data1h.csv", 12, 40)
  o.createChartImage("C:/projects/menus/kodatrades/data/chart5m.png", 40)
//  o.createManifeshAndGitPush()