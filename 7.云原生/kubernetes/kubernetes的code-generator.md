生成自定义资源的client API

  

code-generator提供了以下工具为kubernetes中的资源生成代码:

`deepcopy-gen`: 生成深度拷贝方法,避免性能开销

`client-gen`:为资源生成标准的操作方法(get,list,create,update,patch,delete,deleteCollection,watch)

`informer-gen`: 生成informer,提供事件机制来相应kubernetes的event

`lister-gen`: 为get和list方法提供只读缓存层