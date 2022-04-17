# GithubSearchUsers
用户在输入框中输入有效内容并点击搜索按钮，程序会将查询到的相关结果渲染在列表中。

# 功能模块
+ 使用axios发送ajax请求

# 效果图
![image](https://user-images.githubusercontent.com/41555864/163707380-01153fdb-c744-4428-9f33-9ddb240c74dc.png)

# 组件拆分
- App.vue：掌管所有组件；
- Search.vue：接收用户输入的有效内容并发送ajax请求；
- List.vue：将请求到的数据渲染在列表项中；


# 版本改进
+ src_pubsub：使用发布订阅完成兄弟组件通信（List.vue和Search.vue）
+ src：使用全局事件总线完成兄弟组件通信（List.vue和Search.vue）


# 外部库
+ pubsub：发布订阅消息

# 快速启动

## Project setup
```
npm install
```

## Compiles and hot-reloads for development
```
npm run serve
```
