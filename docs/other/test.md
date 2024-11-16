!!! note "这是 note 类型的提示框"
提示：更多精彩内容记得关注我啊

!!! success "这是 success 类型的提示框"
成功！

!!! failure "这是 failure 类型的提示框"
失败！

!!! bug "这是 bug 类型的提示框"
发现一个 bug，请尽快修复！

??? note "这是 note 类型的提示框"
提示：更多精彩内容记得关注我啊

    第二行
    
    第三行
    
    第四行
    
    第五行
    ...

参考：
https://squidfunk.github.io/mkdocs-material/reference/admonitions/#admonition-icons-octicons

Typora插件展示：

```marp
---
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
---

![bg left:40% 80%](https://marp.app/assets/marp.svg)

# **Marp**

Markdown Presentation Ecosystem

https://marp.app/

---

# How to write slides

Split pages by horizontal ruler (`---`). It's very simple! :satisfied:
```

> [!NOTE]
> Support Type: TIP、BUG、INFO、NOTE、QUOTE、EXAMPLE、CAUTION、FAILURE、WARNING、SUCCESS、QUESTION、ABSTRACT、IMPORTANT



```abc
X:1
T:Twinkle, Twinkle, Little Star
M:4/4
L:1/4
K:C
G2 G2|A2 A2|B2 B2|c3 z|G2 G2|A2 A2|B2 G2|c3 z||
```



```calendar
// 提供内置变量:
//   1. calendar: calendar实例
//   2. Calendar: Calendar类
//   3. option:   calendar的option
//   4. this:     calendar插件实例
// example：https://nhn.github.io/tui.calendar/latest/tutorial-06-daily-view
// API: https://github.com/nhn/tui.calendar/blob/main/docs/en/apis/options.md
// 代码块里的所有内容都会被eval，请注意安全问题
// 可以使用如下注释设置图表宽高（否则使用默认）：
// {height: "800px", width: ""}

const today = new Date();
const yesterday = new Date(today.getTime() - 24 * 60 * 60 * 1000);
const nextMonth = new Date(today.getFullYear(), today.getMonth() + 1, 1);

option = {defaultView: 'week'};
calendar.createEvents([
    {id: 'event1', calendarId: 'cal2', title: 'meeting', start: yesterday, end: today},
    {id: 'event2', calendarId: 'cal1', title: 'appointment', start: yesterday, end: nextMonth},
]);
```



```wavedrom
// 教程: https://wavedrom.com/tutorial.html
// 代码块里的所有内容都会被eval，请注意安全问题
// 可以使用如下注释设置图表宽高（否则使用默认）：
// {height: "300px", width: ""}
{
    signal: [
        { name: "pclk", wave: 'p.......' },
        { name: "Pclk", wave: 'P.......' },
        { name: "nclk", wave: 'n.......' },
        { name: "Nclk", wave: 'N.......' },
        { name: 'clk0', wave: 'phnlPHNL' },
        {},
        { name: 'clk1', wave: 'xhlhLHl.' },
        { name: 'clk2', wave: 'hpHplnLn' },
        { name: 'clk3', wave: 'nhNhplPl' },
        { name: 'clk4', wave: 'xlh.L.Hx' },
    ],
    config : { "hscale" : 1.4 }
}
```



```chart
// 提供内置变量:
//   1. Chart:   chart类
//   2. config:  chart的config
//   3. this:    chart插件实例
// API：https://chart.nodejs.cn/docs/latest/configuration/
// 代码块里的所有内容都会被eval，请注意安全问题
// 可以使用如下注释设置图表宽高（否则使用默认）：
// {height: "300px", width: ""}

config = {
  type: "bar",
  data: {
    labels: ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
    datasets: [{
      label: "# of Votes",
      data: [12, 19, 3, 5, 2, 3],
      backgroundColor: [
        "rgba(255, 99, 132, 0.2)", "rgba(54, 162, 235, 0.2)", "rgba(255, 206, 86, 0.2)",
        "rgba(75, 192, 192, 0.2)", "rgba(153, 102, 255, 0.2)", "rgba(255, 159, 64, 0.2)"
      ],
      borderColor: [
        "rgba(255, 99, 132, 1)", "rgba(54, 162, 235, 1)", "rgba(255, 206, 86, 1)",
        "rgba(75, 192, 192, 1)", "rgba(153, 102, 255, 1)", "rgba(255, 159, 64, 1)"
      ],
      borderWidth: 1
    }]
  }
}
```



```echarts
// 提供内置变量:
//   1. myChart: echarts实例
//   2. echarts: echarts模块
//   3. option:  echarts实例的option
//   4. this:    echarts插件实例
// 更多示例：https://echarts.apache.org/examples/zh/index.html#chart-type-line
// 代码块里的所有内容都会被eval，请注意安全问题
// 可以使用如下注释设置图表宽高（否则使用默认）：
// {height: "300px", width: ""}

option = {
    tooltip: { trigger: 'item' },
    legend: { top: '5%', left: 'center' },
    series: [{
        name: 'Access From',
        type: 'pie',
        radius: ['40%', '70%'],
        avoidLabelOverlap: false,
        label: { show: false, position: 'center' },
        emphasis: { label: { show: true,  fontSize: 40,  fontWeight: 'bold' } },
        labelLine: { show: false },
        data: [
            {value: 1548, name: 'Search Engine'},
            {value: 735, name: 'Direct'},
            {value: 580, name: 'Email'},
            {value: 484, name: 'Union Ads'},
            {value: 310, name: 'Video Ads'}
        ]
    }]
}
```



```timeline
# 使用一级标题表示 timeline 的标题

## 2022-10-1
### 使用二级标题表示时间，三到六级标题表示内容
支持简单的 markdown 语法
- 这是无序列表项 1
- 这是无序列表项 2
---
支持 **加粗**，*斜体*，`代码`，~~删除~~，[链接](https://github.com/obgnail/typora_plugin)，![图片](https://avatars.githubusercontent.com/u/48992887?s=96&v=4)
不支持代码块，因为开发者不希望代码块发生嵌套

## 2023-10-1
语法是开发者自定义的，谨慎使用。
```



```chat
---
# 配置
# 进入严格模式（不忽略语法错误）
useStrict: false
# 展示用户名
showNickname: true
# 展示头像
showAvatar: true
# 不允许展示时间
notAllowShowTime: false
# 允许使用markdown语法
allowMarkdown: true
# 右侧发送者的用户名
senderNickname: me
# 时间的用户名
timeNickname: time
# 用户头像
avatars:
  me: https://avatars.githubusercontent.com/u/48992887?s=96&v=4
  nickname1: ./assets/1.jpg
---

time: 昨天 18:21

testUser1: 使用冒号分割用户名和消息

me: 右侧的用户名为 me，时间为 time。

me: 支持部分 markdown 语法。比如 **加粗**，*斜体*，`代码`，~~删除~~，[链接](https://github.com/obgnail/typora_plugin)，\n![图片](https://avatars.githubusercontent.com/u/48992887?s=96&v=4)

nickname1: 支持使用 yaml 格式的 front matter 修改配置（就和 markdown 一样）\n\n其中的 avatars 选项用于配置用户的头像，如果没有配置头像，默认为用户名的首字符\n\n你可以试试在本文件所属目录下添加 `./assets/1.jpg` 文件，便可以看到对应用户的头像被修改了

注意: 支持导出成 HTML、PDF 等格式。语法是插件开发者自定义的，不具备通用性
```



```kanban
use strict
# Today's task

## Todo
* 语法说明(一级标题表示看板标题\n二级标题表示看板\n- 或 * 表示任务)
- 描述框样式(支持在描述框添加 markdown 行内样式：\n**加粗**，*斜体*，`代码`，~~删除~~，[链接](https://github.com/obgnail/typora_plugin)，![图片](https://avatars.githubusercontent.com/u/48992887?s=96&v=4))
- 严格模式(在首行添加 use strict 进入严格模式，将不会忽略语法错误)
- 当描述为空时隐藏描述框

## In-Progress
- 数量、配色(看板和任务都可以无限添加\n\n可以前往配置修改你喜欢的颜色)
- 当任务数量太多，出现滚动条时(可以将鼠标置于看板下，使用【鼠标滚轮】滚动任务)
- 当看板数量太多，出现滚动条时(可以将鼠标置于看板下，使用【ctrl+鼠标滚轮】滚动看板)

## Completed
- NOTE(语法是插件开发者定义的，无法通用，只建议【每日任务】临时使用)
```



