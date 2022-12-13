# metrics types

Metrics记录值类似于保存在prometheus数据，最终使用还是要通过dashboard类似于grafana进行可视化。


metric_name = table
metric_value  = data value
tags = columns 


1. COUNT, RATE ( is a float between 0 and 1:) :  incr+  decr-

2. GUAGE 单值  :set



SET 不重复数

HISTOGRAM，TIMER   保存这个值的同时会计算出来下面的指标值（AGGREGATION）

    avg,count,median,95percentile,max

timer 是 is an implementation of histogram 只关注时间的histogram

DISTRIBUTION (正态) 

同时计算以下的值（AGGREGATION）
`
	`sum`, `count`, `average`, `minimum`, `maximum`, `50th percentile` (median), `75th percentile`, `90th percentile`, `95th percentile` and `99th percentile`.`