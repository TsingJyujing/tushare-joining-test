# TuShare高级开发者交流群入群测试
## 前言

本群是使用、维护、开发以及二次开发TuShare的交流群，要求群成员有一定的**编程能力和数学能力**，所以设置了一个略微麻烦的入群问题，需要想办法统计一些指标，并且将找出指标的最大值才可以入群。

**本群入群绝对不收一分钱，只需要你证明你自己的技术！**

如果你足够牛，并不想做这么弱智的题目（我承认题目其实不难），可以把自己的项目开源到Github，然后和我或者米哥交流入群（有点像面试的形式）。

这个题目你可以用任何方式来完成，当然任何语言都可以，从C到Hashell都是OK的。

题目的结果就是入群问题，正确的回答入群问题就可以进群，管理员不会拦着任何解出问题的人入群（群满除外），也不会主动T人，但是有以下几种情况例外：
 
1. 日常不聊技术，只聊选股或者闲扯的；
2. 在群内说脏话，人身攻击的；
3. 经查实，不是依靠自己计算获取答案的；
4. 公布自己解出的答案的；

加入这个群以后，讨论的内容会更加深入。
我也会从群中招募，共同组织一个开源团队开发一些数据分享、分析或者可视化的项目。
总而言之，有多种玩法。

祝大家玩的开心！

**群号：664829324**

**本人QQ号：1344413992**

## 正题
大概的内容就是需要计算2017年12月份股票波动率（部分股票无法计算就忽略）最大的一支股票，然后这个股票的代码就是入群的密码。

### 波动率计算方法
（很抱歉Github上不能用LaTeX，我使用符合习惯的表达式描述计算方式）
1、收益率计算方法：
收益率u=ln(close_price/open_price)
2、波动率定义：
波动率是收益率的标准差。
标准差的定义是sqrt(sum((u-mean(u))^2)/(n-1))
其中n是数据条数数量。
3、当月数据量少于3条的可以不计算波动率。

### API说明
考虑到有些同志经常被BAN，直接使用TuShare的接口不能正常访问就坑爹了，我特地准备了一套接口给大家使用，但是这个接口调用的时候有一定的失败概率（是我特意设定的喵），大家需要编写错误处理程序。
下面是我对外开放的API的文档。

#### 获取股票列表的API
参考链接：[http://tusharetest.lovezhangbei.top/api/codes](http://tusharetest.lovezhangbei.top/api/codes) 
返回格式为JSON，返回结果中，status是成功（success）还是失败（fail/error）的标记，codes是所有的股票代码
```json
{
  "codes": [
    "300250",
    "600048",
    ....,
    "300482",
    "002243",
    "002087",
    "000571"
  ],
  "status": "success"
}
```
#### 获取单个股票12月日线数据的API
参考链接：[http://tusharetest.lovezhangbei.top/api/k/daily?code=000002](http://tusharetest.lovezhangbei.top/api/k/daily?code=000002) 
返回格式为JSON，返回结果中，status是成功（success）还是失败（fail/error）的标记，code是输入的股票代码，data是所有的数据。
```json
{
  "code": "000002",
  "data": [
    {
      "volume": 557438.0,
      "tick": "2017-12-01",
      "open": 30.5,
      "close": 30.73,
      "low": 30.5,
      "high": 32.03
    },
    {
      "volume": 379890.0,
      "tick": "2017-12-04",
      "open": 30.6,
      "close": 30.85,
      "low": 29.9,
      "high": 31.3
    },
    ......,
    {
      "volume": 385307.0,
      "tick": "2017-12-29",
      "open": 30.75,
      "close": 31.06,
      "low": 30.74,
      "high": 31.71
    }
  ],
  "status": "success"
}
```