

### 快速掌握Beego 

1. [快速入门](https://beego.me/quickstart)
2. 通过视频快速掌握Beego用法，马斯的免费慕课课程[使用Beego构建完整web项目](https://www.imooc.com/learn/1053)

### 实验项目

水文局每天要检测钱塘江水位的高度，在钱塘江部署了水位高度采集器，每天凌晨会采集水位高度，该采集器已经联网，每天会向水位管理系统报告今日水位高度h。管理系统的监控页面，可以显示今天水位高度，以及当前水位在过去X天内的水位的百分位位置p，百分位的含义是代表了今天水位，在过去X天内的水位水平。同时，它还提供了1个查询接口，可以查询过去Y天的水位高度h和百分位位置p。


举例：
```
2020-07-03 1
2020-07-04 2
2020-07-05 4
2020-07-06 3
```

过去4天的水位数组为：[1,2,4,3]，3的百分位位置为75%，因为过去有3天小于等于3，所以百分位比率为：3天/4天=75% 。

你需要完成1个水位管理系统，它有2个功能：
1. 接收水位高度采集器上报的高度h，计算今天的水位百分位，并把它存储到MySQL。
2. 查询过去Y天的水位高度h和百分位位置p。

这2个功能分别是2个HTTP API，请求和响应都是JSON格式：
1. `/height`: 是POST操作，有2个字段：日期、高度。响应为2个字段，status：取success或者fail，error：fail的原因。
2. `/height`: 是GET操作，只有1个字段：天数Y，即过去Y天的记录。响应为JSON数组，每一项为3个字段：日期、高度、过去X天的百分位p。

管理系统配置项：
1. `dayrange`：代表上文描述中的X。

提醒：
1. 不需要实现前端，http请求使用Postman发送即可。
2. 百分位位置可以使用Go语言科学计算库的[Quantile](https://godoc.org/gonum.org/v1/gonum/stat#Quantile)完成，该函数可以计算一组值的百分位数，通过百分位数想办法计算出某个值在数组中的百分位位置。
