# 关于浏览器缓存策略

## 文档

http://blog.csdn.net/eroswang/article/details/8302191

## 注意点

0. 当response header 设置 Cache-Control:max-age=0 时，如果存在Last-Modified与ETag，页面依旧会出现304缓存问题；

## 设置值

### html 304缓存

0. Expires 设置为一个过期时间； 

0. Last-Modified 与 ETag 设置；

### 静态资源

0. Expires 设置为一个未来时间；

0. ETag 不设置

### 强制不缓存

0. Cache-Control:no-store