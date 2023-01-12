##  0. 概览
在核心指标一文里面讲到，LCP 主要受四个因素影响：

-   服务器响应速度
-   JavaScript 和 CSS 渲染阻塞
-   资源加载时间-图像、字体、视频等资源
-   客户端渲染速度

下面逐个进行分析


##  1. 服务器响应速度 
参考 性能优化-性能指标 TTFB

##  2. JavaScript 和 CSS 渲染阻塞
### 2.1 减少CSS阻塞
-   压缩CSS  
    去掉空格、缩进、注释等，可以使用打包插件支持
-   延迟加载非关键 CSS  
    使用Chrome代码覆盖率查看是否使用CSS  
    初始页面渲染不需要的CSS可以使用 loadCSS 来异步加载文件  
    ```html
    <link rel="preload" href="stylesheet.css" as="style" onload="this.rel='stylesheet'">
    ```
-   内联关键 CSS  
    通过把用于首屏内容的任何关键路径 CSS 直接包括在<head>中来将这些 CSS 进行内联  
    如果您无法为您的网站手动添加内联样式，请使用库来将该过程自动化  
    Critical、CriticalCSS 和 Penthouse 都是提取和内联首屏 CSS 的包  
    Critters 是一个 webpack 插件，能够内联关键 CSS 并对其余部分进行懒加载

### 2.2 减少JavaScript阻塞时间  
-   压缩js文件  
-   延迟加载未使用的js文件  
更多参考 FID优化
    
##  3. 资源加载速度
根据影响 LCP 的元素类型，有几种方法可以确保尽快加载这些元素：

### 3.1 优化和压缩图像  
-   首先考虑不使用图像。如果图像与内容无关，请将其删除。  
-   压缩图像（例如使用 Imagemin）  
-   将图像转换为更新的格式（JPEG 2000、JPEG XR 或 WebP）  
-   使用响应式图像，适配不同分辨率  
-   使用图像 CDN 缓存
    

### 3.2 预加载重要资源
使用preload预加载字体、图片或视频  
```html
<link rel="preload" as="script" href="script.js" />
<link rel="preload" as="style" href="style.css" />
<link rel="preload" as="image" href="img.png" />
<link rel="preload" as="video" href="vid.webm" type="video/webm" />
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin />
```

### 3.3 压缩文本文件
压缩诸如 Gzip(兼容性好) 和 Brotli(更优更新) 之类的算法可以显著缩减在服务器和浏览器之间传输的文本文件（HTML、CSS、JavaScript）大小   
可以在构建时提前压缩好


### 3.4 自适应服务  
根据用户设备和网络环境决定加载哪种资源  
```javascript
if (navigator.connection && navigator.connection.effectiveType) {
  if (navigator.connection.effectiveType === '4g') {
    // 4G网络加载视频
  } else {
    // 非4G网络加载图像
  }
}
```

navigator.connection.effectiveType：有效连接类型  
navigator.connection.saveData：启用/禁用数据保护程序  
navigator.hardwareConcurrency：CPU 核心数  
navigator.deviceMemory：设备内存  

### 3.5 使用 Service Worker 缓存资源  
参考Service Worker


##  4. 优化客户端渲染 
单页应用，如React、Vue和Angular，需要注意大型JavaScript包对LCP的影响  

### 4.1 最小化关键 JavaScript 
参考本章2.2部分

### 4.2 使用服务端渲染  
弊端：

-   增加复杂性  
-   增加服务器响应时间 (首字节时间 TTFB)  
-   Time to Interactive 可交互时间 (TTI) 变得更糟  

### 4.3 使用预渲染  
使用无头浏览器在构建期间生成每个路由的静态HTML文件 

##  5. LCP优化总结 

考虑到实际业务中，框架选择、SSR、CDN、后端服务等外部条件通常都难以改变  
前端开发通常只能根据情况选中以上的一部分手段进行优化