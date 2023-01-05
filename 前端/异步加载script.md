### sync - 同步脚本
- 下载：阻塞代码
- 执行：同步执行

### async - 异步脚本
- 下载：不阻塞代码
- 执行：立即同步执行
- 页面Load事件前执行，DOMContentLoaded事件顺序不确定
- 执行顺序依赖网络传输
- 不建议修改DOM，可能获取不到

### defer - 延迟脚本
- 下载：不阻塞代码
- 执行：页面解析完成后执行
- 建议只包含一个延迟脚本


### 加载

![1672819126136.png](https://note.youdao.com/yws/res/108/WEBRESOURCEec4c321250261e9324fdf00468279d8c)

### 执行
![dx-20230104@2x.png](https://note.youdao.com/yws/res/122/WEBRESOURCE773bedf0d276206d45fc284b0f0ebd7b)

### 注意
- 内联脚本都是同步脚本，包括动态生成的
- 内联代码可以用URL.createObjectURL 包装的 Blob 对象支持异步