

## 什么是HTTP缓存
HTTP 缓存存储与请求关联的响应，并将存储的响应复用于后续请求

## HTTP缓存的优势
1. 响应速度快
2. 减少服务端负载
3. 减轻网络压力(对整个网络的好处)

## HTTP缓存的种类

根据[HTTP缓存标准](https://httpwg.org/specs/rfc9111.html#caching)，分为两类

- 私有缓存  
  通常是浏览器缓存， 存储的响应不与其他客户端共享，可以存储该用户的个性化响应

- 共享缓存  
  存储能在用户之间共享的响应，共享缓存可以进一步细分为代理缓存和托管缓存，比如CDN缓存


## 浏览器缓存  

### 直接缓存
一般是基于时间的缓存
1. 指定有效期    
   Cache-Control: max-age=315360000 (HTTP1.1首选)
2. 指定过期时间   
   Expires: Tue, 28 Feb 2022 22:22:22 GMT
3. 缓存策略  
   Vary: Accept-Language  
   缓存基于响应 URL 和 Accept-Language请求标头的组合进行键控，而不是仅仅基于响应 URL


### 协商缓存 

1. Last-Modified/If-Modified-Since  
   存在问题：时间格式、时区等问题、分布式服务器的时间同步问题 
2. ETag/If-None-Match



### CDN缓存

### 缓存破坏
1. 对于子资源， 静态资源通常内容不变，每次变化后都生成新的URL  
2. 对于主要HTML资源，不适用缓存破坏，Cache-Control: no-cache, private
3. favicon.ico、manifest.json、.well-known 和无法使用缓存破坏更改 URL 的 API 端点也不适用

| Col1 | Col2 | Col3 | Col4 |
| ---- | ---- | ---- | ---- |
| d    |      | d    |      |
| d    |      |      |      |
| d    |      |      |      |
| d    |      |      |      |
