### Commit message格式
```
():
```

#### type（必选）
用于说明 commit 的类别，只允许使用下面的标识：

- feat：新功能（feature）
- fix/to：修复bug，可以是QA发现的BUG，也可以是研发自己发现的BUG
 - fix: 产生diff并自动修复此问题。适合于一次提交直接修复问题
 - to: 只产生diff不自动修复此问题。适合于多次提交。最终修复问题提交时使用fix
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- perf：优化相关，比如提升性能、体验
- test：增加测试
- chore：构建过程或辅助工具的变动
- revert：回滚到上一个版本
- merge：代码合并
- sync：同步主线或分支的Bug

#### scope（可选）
scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

例如在`Angular`，可以是`$location`, `$browser`, `$compile`, `$rootScope`, `ngHref`, `ngClick`, `ngView`等。

如果你的修改影响了不止一个`scope`，你可以使用`*`代替。

#### subject
`subject`是 commit 目的的简短描述，不超过50个字符。

其他注意事项：

- 建议使用中文
- 结尾不加句号或其他标点符号

### 提交示例
```
feat 完成什么新功能
fix 修改什么bug
refactor(Service) 重构……
feat:完成什么新功能
```
注意：监控服务只监控开头是否有关键字，后面是否有描述信息，比如：[type][空格][描述信息]；冒号可有可无，有冒号可以没有空格，必修保证type和描述信息之间有分隔符。没有做具体方面的要求，这样也利于不同团队根据自己的需求定制自己的规范信息