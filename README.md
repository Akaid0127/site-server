# 仿掘金站点简易后端

## 介绍

使用 `json-server` 搭建的完整模拟 REST API 接口



## 环境搭建

1、安装 node

https://nodejs.org/en/



2、安装 json-server

```shell
npm install -g json-server
```



3、启动服务，加载静态资源

```shell
json-server site.json --static ./source
```



## 服务接口

请求接口：

```
// 用户
http://localhost:3000/users
// 管理员
http://localhost:3000/admin
// 主导航标签
http://localhost:3000/nav
// 文章类型标签
http://localhost:3000/types
// 文章
http://localhost:3000/articles
// 作者榜
http://localhost:3000/topUsers
```



请求方法：

- 数据查询要使用 `GET`
- 新增数据要使用 `POST`
- 删除数据要使用 `DELETE`
- 修改数据使用 `PUT` 和 `PATCH`







