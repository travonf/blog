---
title: JavaScript基础
date: 2018-12-05 23:15:46
tags: "javascript"
---

window.innerHeight 	表示窗口高度
$(document).height() 	返回文档高度（当前显示的高度）
$(document).scrollTop() 	返回滚动条与顶部的距离,在最上部时为0,
	在最下部时为:$(document).height()-window.innerHeight


$(document).scrollTop($(document).height()-window.innerHeight);
