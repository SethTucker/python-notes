# Safety Stock Analysis

<br>

export to csv
```
Inventory class
    list of Skus
    overview stuff, like top 10, rank of units ordered
    
Sku class
    Name
    ABC_XYZ_Classification - https://github.com/KevinFasusi/supplychainpy/blob/5bffccf9383045eace82ee1d21ca49e1ecdd7d22/supplychainpy/inventory/abc_xyz.py#L154
    Coefficient of variation (demand_variability) - std_dev/mean - https://blog.arkieva.com/do-you-use-coefficient-of-variation-to-determine-forecastability/
    Insights - insights from pics
    Mean - daily + monthly
    list Orders
    const Service level - 99.6
    standard_deviation - daily and monthly
    const Z-Score - 99.6

    Optional:
    lead time
    reorder_level
    reorder_quantity
```
```
1) W0
2) MDMK
3) idk

Enter a #: 
```

<br>

### Dataset format:
- SKU = color
- Month = qty ordered

Sku | mar | apr | may | jun | jul | aug | unit cost | lead-time | retail_price | qty_on_hand | backlog
--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---
Blue | 2665 | 1841 | 1231 | 2598 | 1988 | 1988 | 1001 | 2 | 5000 | 1003 | 10

<br>

[Full dataset example of 40 SKUs](https://github.com/KevinFasusi/supplychainpy/blob/master/supplychainpy/sample_data/complete_dataset_small.csv)

<br>
<br>

## Example Analysis
```
SKU: KR202-209

Average Qty Ordered: 2053  
Standard Deviation: 644 (Average Qty Ordered = 2053+or-644)  
Demand Variability: 0.314

Qty on Hand: 1003  
Calculated Safety Stock: 1165

Reorder Level: think these 2 got messed up
Reorder Qty: 
formula = Lead_time*Demand+Service_level*Std_Dev*sqrt(Lead_time)

Economic Order Qty: 44  
Economic Order Variable Cost: $15,708

ABC XYZ Classification: BY
(Medium consumption value. Predictably variable demand. Less reliable forecasts.)

Excess stock: 0  
Shortage units: 5979

Total Qty Ordered: 24,638  
Revenue: $123,190

Min Ordered Month: 731  
Max Ordered Month: 2927  
Inventory Turns: 24  
Inventory Traffic Light: Green (inventory to cover demand for next 7 days and up to safety stock)
```

<br>

Comparing with the other SKUs in the dataset:
```
Revenue Rank: 19/40  
Excess Rank: 6/40  
Shortage Rank: 15/40  
Safety Stock Rank: 29/40  
Unit Cost Rank: 21/40
```

<br>
<br>

## Other easy analysis
Get list of all 'AY' class SKUs:
```
KR202-229
KR202-232
KR202-234
KR202-235
KR202-239
KR202-242
```

<br>

Get revenue of all 'CZ' class SKUs:
```
Total CZ Revenue: $5,724,966
```

<br>

Average monthly order qty of all SKUs:
```
1601.44
```

<br>

SKUs with largest safety stock:
```
#1 KR202-241 - Safety stock: 2719
#2 KR202-231 - Safety stock: 2484
#3 KR202-233 - Safety stock: 2472
#4 KR202-227 - Safety stock: 2277
#5 KR202-225 - Safety stock: 2261
```

<br>
<br>
<br>

## Forecast testing
```
    alpha     demand   forecast_error   level_estimates    one_step_forecast
0   0.00689     104    -1531.454545      1624.903085        1635.454545
1   0.00689    2262      637.096915      1629.292574        1624.903085
2   0.00689     350    -1279.292574      1620.478467        1629.292574
3   0.00689     528    -1092.478467      1612.951476        1620.478467
4   0.00689    2570      957.048524      1619.545377        1612.951476
5   0.00689    1216     -403.545377      1616.765019        1619.545377
6   0.00689    1101     -515.765019      1613.211486        1616.765019
7   0.00689    2755     1141.788514      1621.078214        1613.211486
8   0.00689    2856     1234.921786      1629.586614        1621.078214
9   0.00689    2381      751.413386      1634.763724        1629.586614
10  0.00689    1867      232.236276      1636.363792        1634.763724

    squared_error   t   regression
0    2.345353e+06   1   602.090909
1    4.058925e+05   2   826.581818
2    1.636589e+06   3  1051.072727
3    1.193509e+06   4  1275.563636
4    9.159419e+05   5  1500.054545
5    1.628489e+05   6  1724.545455
6    2.660136e+05   7  1949.036364
7    1.303681e+06   8  2173.527273
8    1.525032e+06   9  2398.018182
9    5.646221e+05  10  2622.509091
10   5.393369e+04  11  2847.000000
```
![](https://supplychainpy.readthedocs.io/en/latest/_images/image3.png)

<br>
<br>
<br>

## Creating Supply Chain Simulation
https://dc.etsu.edu/cgi/viewcontent.cgi?article=4651&context=etd  
https://supplychainpy.readthedocs.io/en/latest/monte_carlo_simulation.html  
[YT Part 1](https://www.youtube.com/watch?v=7LuN_6m7h2o) [Part 2](https://www.youtube.com/watch?v=Kmu9DNQamLw)  
[Part 1](https://codereview.stackexchange.com/questions/27874/inventory-simulation-using-pandas-dataframe)  
[Part 2](https://github.com/Jdash99/sinvi)  
[Part 3](https://translate.google.com/translate?sl=auto&tl=en&js=y&prev=_t&hl=en&ie=UTF-8&u=https%3A%2F%2Fsinvi.readthedocs.io%2Fen%2Flatest%2Fintroduccion.html&edit-text=)  

<br>
<br>
<br>

#### Links:
https://supplychainpy.readthedocs.io/en/latest/index.html  
[Example](https://www.udemy.com/safety-stock-inventory-control/)

https://link.springer.com/content/pdf/10.1007%2F978-0-387-74157-4_39.pdf

http://web.mit.edu/2.810/www/files/readings/King_SafetyStock.pdf

https://msdn.microsoft.com/en-us/magazine/mt683796.aspx

https://www.cgma.org/resources/tools/cost-transformation-model/abc-xyz-inventory-management.html
