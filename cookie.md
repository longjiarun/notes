# cookie 中的坑 （只针对chrome）

## 常见的坑

- 1、cookie并不是每个域名下4K限制，而是每个路径下；

- 2、cookie最大值不一定是4K；

- 3、cookie会随每个请求发送到后端（包括父域），所以不宜设置过多cookie；

- 4、cookie如果未设置expires，浏览器关闭以后cookie并不一定会被清空；


## 读cookie

- 1、同一域名下，首先读取当前路径下的cookie。如当前路径下无cookie，则依次往上级目录（不包含根目录）读取；


```javascript

//默认写到根路径下
cookie("name","child1");	

//写到当前路径下
cookie("name","child2",{
	path:"./"
});	

console.log(cookie("name"));
//输出 child2

```

- 2、父子域名存在相同cookie的情况下，如当前域名下的当前目录且上级目录（不包含根目录）未存在cookie，则默认读取最先被修改的 cookie（谁最先赋值，读取最先赋值的cookie）。

```javascript

第一种情况

//默认写到根路径下
cookie("name","child1");	

//写到父域名下
cookie("name","parent",{
	domain:"weidian.com"
});	

console.log(cookie("name"));
//输出 child1


第二种情况

//写到父域名下
cookie("name","parent",{
	domain:"weidian.com"
});	

//默认写到根路径下
cookie("name","child1");	


console.log(cookie("name"));
//输出 parent


第三种情况

//写到父域名下
cookie("name","parent",{
	domain:"weidian.com"
});	

//默认写到根路径下
cookie("name","child1");	


//默认写到当前路径下
cookie("name","child2",{
	path:"./"
});	

console.log(cookie("name"));
//输出 child2
```

## 写cookie

- 1、不传递path，则默认写到当前路径下；

- 2、不传递domain，则默认写到当前域名下；

- 3、不传递 expires，则大多数浏览器关闭会清除cookie；

## 删除cookie

参照[写cookie](#写cookie)