## 配置代理

```shell
GOPROXY=https://goproxy.cn,direct
```

## 下载Gin

```shell
go get -u github.com/gin-gonic/gin
```

## HelloWorld

```go
package main

import "github.com/gin-gonic/gin"

func Index(context *gin.Context) {
	context.String(200,"hello world")
}

func main()  {
	// 创建一个默认的路由
	router := gin.Default()

	// 绑定路由规则和路由函数 访问/index的路由 将由 对应的函数去处理
	//router.GET("/index", func(context *gin.Context) {
	//	context.String(200,"hello world")
	//})
	router.GET("/index",Index)

	// 启动监听 gin会将web服务运行在本机的端口
	err := router.Run(":8080")
	if err != nil {
		return 
	}
}

```

1. `router := gin.Default` :这是默认服务器。使用gin的`Default`方法创建一个路由`Handler`;
2. 然后通过Http方法绑定路由规则和路由函数。不同于`net/hhtp`库的路由函数,gin进行了封装，把`request`和`response`都封装到了`gin.Contex`t的上下文
3. 最后启动路由的Run方法监听端口。还可以用`http.ListenAndServe(":8080",router)`,或者自定义Http服务器配置

## 两种启动方式

```go
router.Run(":8080")
http.ListenAndServe(":8080",router)
```

`router.Run` 本质就是`ListenAndServe`的封装

## 响应

### 状态码

| 状态码 | 含义      |
| ------ | --------- |
| 200    | 正常      |
| 404    | Not Found |
|        |           |