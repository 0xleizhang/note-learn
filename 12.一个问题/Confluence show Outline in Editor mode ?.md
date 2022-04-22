使用confluence的时候发现编辑状态右侧不能同步显示outline，习惯了这个特性，比如语雀，obsidian都有。

需要的原因：
1. 主要是文档内容较多时，需要快速跳转
2. 更多的时候写文档的时候可能会先写大纲，金字塔思维进行输出文档，实时的能在右侧看到整体结构

搜了一下也有人有类似的需求：

https://community.atlassian.com/t5/Confluence-questions/Document-Outline-Navigation-in-Editor/qaq-p/1351188


经过搜索可以确定的是Confluence本身没有这个功能。

可以考虑通过chrome插件实现一个。或者利用油猴（**Tampermonkey**）写一个。

有油猴！
参考confluence的一些代码 https://www.userscript.zone/search?source=header&q=confluence
