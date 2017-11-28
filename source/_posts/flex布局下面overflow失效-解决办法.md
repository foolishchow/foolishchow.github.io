---
title: flex布局下面overflow失效 解决办法
date: 2017-11-28 15:08:58
tags: []
---

## Firefox下flex元素overflow失效的原因和修复
>使用flex布局时，有些需要滚动显示全部内容的元素在Firefox下却不能滚动，
>其原因在于overflow失效。

- 解决方法：   
给该元素添加`min-height: 0`或者`min-width: 0`，取决于你的滚动方向，如果无效，尝试给其父元素添加该`style`，以此类推。
- 原因：   
在`firefox`下，`flex`元素默认将其最小尺寸设置为其子元素的尺寸，这意味着父元素永远能显示全部子元素，即使这样导致整个页面超过了屏幕。这还`overflow`个鬼嘛！。因此我们需要覆盖默认的最小尺寸。
`firefox`的这一设定可以参见[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)
>为了确保弹性项目有合理的默认最小尺寸，使用 min-width:auto 与 min-height:auto。   
对于弹性项目，属性值 auto 使项目的最小宽/高在计算中不会小于其内容的实际宽/高，这样可以保证项目渲染得足够大以容纳其内容。   
更多细节请参考 min-width 与 min-height 。
