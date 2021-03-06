# DataBase Records

在这里将可能用到的所有数据集和资源集进行划分和罗列.

## 数据库总览

首先,我们需要对我们要做的系统进行明确的定位和大概的设计:

定位在于: **事件**

看似一场大戏的事件,以 `角色`, `时间`, `地点`, `事件` 的结构进行数据库的基本搭建.

### 角色/实体

> 实体: 客观存在并可相互区别的事物

实体可分为 自然人, 家族, 公司, 社团, 政府, 党组, 国家等等类别.

这些都是可以用来当作主体来对环境进行操作的具体对象.

### 时间

> 时间: 是物质的运动、变化的持续性、顺序性的表现，包含时刻和时段两个概念.

时间的划分就需要再进行不同的考量了:

- 对于时间点(时刻)的描述相对固定,我们可以采用各种历法进行标识.
- 对于时间段的描述则是各式各样
  - 可以按历法算,如 2020年1月
  - 可以按年号算,如 康熙十三年
  - 也可以按发生重大事件的总体时间来算,如 中世纪

### 地点

对于地点并没有特殊的约定,但是这里必须要说明的是,地点名词和时间的联系是不可分割的,如果单独说了某个地名,那么只能默认为当今情况下的地点.

### 事件

> 事件:  比较重大、对一定的人群会产生一定影响的事情 

事件的描述可简可繁,不必挂上固定的格式

但是所有的事件内容.无非是常用的几种格式,包括但不限于 文字描述, 图片, 音视频, 数据表等等,这也就限定了事件的描述形式.



## 具体设计

### 具体实例

将上述的骨架搭建起来以后,我们可以进行写出一个具体的实例:

```json
{
    role: {
        type: "name",
        at: "李叶飞"
    },
    time: {
        type: "date",
        at: "2020-02-20"
    },
    loc: {
        type: "postition",
        at: "宏昌峻公寓 1#331"
    },
    event: {
        content: "编辑Markdown文件."
    },
    desc: "日常编辑"
}
```

### 简化实例

以上文档可以简化为:

```json
{
    role: "李叶飞",
    time: "2020-02-20",
    loc: "宏昌峻公寓 1#331",
    event: "编辑Markdown文件.",
    desc: "日常编辑"
}
```



### 数据库结构

所以,其实数据库的集合结构可以简单的由四个主要部分和一个备注部分表示.



| 字段名 | 涵义 | 备注 |
| :----- | ---- | ---- |
| role   | 角色 | 必须 |
| time   | 时间 | 必须 |
| loc    | 地点 | 必须 |
| event  | 事件 | 必须 |
| desc   | 备注 |      |

