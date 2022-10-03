  

  

[cdp4j](https://github.com/webfolderio/cdp4j) 收费，API设计的很好

  

[jvppetter](https://github.com/fanyong920/jvppeteer) puppeteer java版，个人项目

  

[**playwright**](https://playwright.dev/java/docs/api/class-page#page-pdf) **微软出品 e2e测试 ✅**

  

[selenium](https://stackoverflow.com/questions/47729046/generate-pdf-with-selenium-chrome-driver) 面向测试 ,未封装，需要通过 chromeDriver 执行 Page.printToPDF 创建

  

本质上都是通过 [devtools protocol](https://chromedevtools.github.io/devtools-protocol/tot/Page/#method-printToPDF) 与浏览器后端通信，各种库充当的是client的角色

原公有云方案：

后台上传json data 到OSS -->

fc 触发器 执行nodejs脚本 [项目](https://code.aone.alibaba-inc.com/middleware-asp/advisor-fc-pre) ->

脚本将OSS json数据设置到 window.__advisor_data ，

使用[advisor-papers](https://code.aone.alibaba-inc.com/advisor/advisor-papers) 项目的前端代码渲染，

打开指定路由 使用 [puppeteer](https://github.com/puppeteer/puppeteer) 截图PDF

上传PDF到OSS

回传完成消息到MQ消息队列

后台消费MQ知道报告执行完成

专有云方案：

定时任务触发Java任务->

任务通过playwright 访问前端渲染报告页面（**前端提供访问地址路径**）

通过playwright 设置window.__advisor_data （渲染所需的数据）

再通过playwright 截图PDF

后端保存PDF截图到OSS

后端完成报告生成




# 其他报告方案

java poi 生成 doc  ，灵活性差，样式效果差

freemarker 生成html  html转成doc  pdf ，灵活性差，样式效果差



