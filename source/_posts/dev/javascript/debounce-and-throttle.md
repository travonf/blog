---
title: 防抖和节流
date: 2008-09-03 09:00:00
updated: 2008-09-03 09:00:00
tags: "javascript"
categories: "Develop"
---

<table>
<colgroup>
<col width="10%">
<col width="45%">
<col width="45%">
</colgroup>
<thead>
<tr>
<td></td>
<td>防抖 debounce</td>
<td>节流 throttle</td>
</tr>
</thead>

<tbody>
<tr>
<td align="center">概念</td>
<td>任务频繁触发的情况下<strong>间隔时间</strong>超过<strong>指定值</strong>的时候才会执行<br />时间间隔不定, 连续不断的触发, 比如校验用户输入<br />在事件被触发n秒后再执行回调，如果在这n秒内又被触发，则<strong>重新计时</strong></td>
<td>任务频繁触发的情况下<strong>指定间隔</strong>内只会执行一次任务<br />时间周期固定<br />规定在一个单位时间内，只能触发一次函数。如果这个单位时间内触发多次函数，只有一次生效。</td>
</tr>

<tr>
<td align="center">理解</td>
<td>函数防抖就是法师发技能的时候要读条，技能读条没完再按技能就会重新读条。<br />必须等读条完毕才能发出技能,否则重新计时, 这个很关键.</td>
<td>函数节流就是fps游戏的射速，就算一直按着鼠标射击，也只会在规定射速内射出子弹。<br /></td>
</tr>

<tr>
<td align="center">场景</td>
<td valign="top">
<ol>
<li>search搜索联想，用户在不断输入值时，用防抖来节约请求资源。</li>
<li>window触发resize的时候，不断的调整浏览器窗口大小会不断的触发这个事件，用防抖来让其只触发一次</li>
</ol>

![debounce1](/blog/images/debounce1.png)

前缘（或者“immediate”）
![debounce2](/blog/images/debounce2.png)

</td>
<td valign="top">
<ol>
<li>鼠标不断点击触发，mousedown(单位时间内只触发一次)</li>
<li>监听滚动事件，比如是否滑到底部自动加载更多，用throttle来判断</li>
</ol>

`|-1-|-3-|-2-|-4-|-2-|-4-|-3-|-0-|-1-|-2-|-3-|-4-|-0-|-1-|`
如上所示:每个时间周期内都可能会有多次任务触发,但是每次只会执行一个,这就是节流,那么如何实现呢?

</td>
</tr>

<tr>
<td align="center">原理</td>
<td valign="top">
<ol>
<li>通过闭包保存setTimeout返回值, </li>
<li>当用户持续输入时, clearTimeout(清理延时任务), </li>
<li>设置新的延时任务</li>
<li>这样可以保证用户持续输入时每次重置延时任务, 等用户停止输入才会开始执行函数</td></li>
</ol>
<td valign="top">
<ol>
<li>通过闭包保存一个标记, 在函数开头判断标记是否可用, 可用执行,否则返回.</li>
<li>外部函数定期执行, 完毕标记重置</li>
</ol>
</td>
</tr>

<tr>
<td align="center">实现</td>
<td>

```javascript
function debounce(fn, interval = 300) {
  let timerID = null;
  function run() {
    if (timerID) clearTimeout(timerID);

    timerID = setTimeout(() => {
      fn.apply(this.arguments);
    }, interval);
  }

  return run;
}
```

</td>
<td>

```javascript
function throttle(fn, interval = 300) {
  let running = false;
  function run() {
    if (running) return;
    running = true;
    timerID = setTimeout(() => {
      fn.apply(this, arguments);
      running = false;
    }, interval);
  }

  return run;
}
```

</td>
</tr>
</tbody>

<tfoot>
<tr>
<td align="center">总结</td>
<td>函数防抖和函数节流都是防止某一时间频繁触发，但是这两兄弟之间的原理却不一样。</td>
<td>函数防抖是某一段时间内只执行一次，而函数节流是间隔时间执行。</td>
</tr>
</tfoot>

</table>
