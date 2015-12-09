title: Crontab的格式
date: 2015-12-03 18:38:36
tags:
---
### Linux Crontab格式
>一个cron表达式有至少5个有空格分隔的时间元素。

```bash
 +---------------- 分 (0 - 59)
 |  +------------- 时 (0 - 23)
 |  |  +---------- 日 (1 - 31)
 |  |  |  +------- 月 (1 - 12)
 |  |  |  |  +---- 周 (0 - 7) (Sunday=0 or 7)
 |  |  |  |  |
 *  *  *  *  *  command to be executed
```
其中：
- 逗号(',') 指定列表值。如: "1,3,4,7,8"
- 中横线('-') 指定范围值 如 "1-6", 代表 "1,2,3,4,5,6"
- 星号 ('*') 代表所有可能的值
- Linux(开源系统似乎都可以)下还有个 "/" 可以用. 在 Minute 字段上，*/15 表示每 15 分钟执行一次. 而这个特性在商业 Unix ，比如 AIX 上就没有. 


### Quartz Crontab格式
>一个cron表达式有至少6个（也可能7个）有空格分隔的时间元素。
Cron表达式对特殊字符的大小写不敏感，对代表星期的缩写英文大小写也不敏感。

```bash
 +------------------- 秒 (0 - 59)
 |  +---------------- 分 (0 - 59)
 |  |  +------------- 时 (0 - 23)
 |  |  |  +---------- 日 (1 - 31)
 |  |  |  |  +------- 月 (1 - 12)
 |  |  |  |  |  +---- 周 (0 - 7) (Sunday=0 or 7)
 |  |  |  |  |  |  -- 年 (1970－2099)
 *  *  *  *  *  *  *    command to be executed
```
其中：
- 逗号(',') 指定列表值。如: "1,3,4,7,8"
- 中横线('-') 指定范围值 如 "1-6", 代表 "1,2,3,4,5,6"
- 星号 ('*') 代表所有可能的值
- 问号（?）：该字符只在日期和星期字段中使用，它通常指定为“无意义的值”，相当于点位符；
- 斜杠(/)：x/y表达一个等步长序列，x为起始值，y为增量步长值。如在分钟字段中使用0/15，则表示为0,15,30和45秒，而5/15在分钟字段中表示5,20,35,50，你也可以使用*/y，它等同于0/y；
- L：该字符只在日期和星期字段中使用，代表“Last”的意思，但它在两个字段中意思不同。L在日期字段中，表示这个月份的最后一天，如一月的31号，非闰年二月的28号；如果L用在星期中，则表示星期六，等同于7。但是，如果L出现在星期字段里，而且在前面有一个数值 X，则表示“这个月的最后X天”，例如，6L表示该月的最后星期五；
- W：该字符只能出现在日期字段里，是对前导日期的修饰，表示离该日期最近的工作日。例如15W表示离该月15号最近的工作日，如果该月15号是星期六，则匹配14号星期五；如果15日是星期日，则匹配16号星期一；如果15号是星期二，那结果就是15号星期二。但必须注意关联的匹配日期不能够跨月，如你指定1W，如果1号是星期六，结果匹配的是3号星期一，而非上个月最后的那天。W字符串只能指定单一日期，而不能指定日期范围；
- LW组合：在日期字段可以组合使用LW，它的意思是当月的最后一个工作日；
- 井号(#)：该字符只能在星期字段中使用，表示当月某个工作日。如6#3表示当月的第三个星期五(6表示星期五，#3表示当前的第三个)，而4#5表示当月的第五个星期三，假设当月没有第五个星期三，忽略不触发；
- C：该字符只在日期和星期字段中使用，代表“Calendar”的意思。它的意思是计划所关联的日期，如果日期没有被关联，则相当于日历中所有日期。例如5C在日期字段中就相当于日历5日以后的第一天。1C在星期字段中相当于星期日后的第一天。

<div class="tip">
后面这几个针对星期的参数，不好记，交流起来都困难。鬼才用，虽然鬼很多。
</div>