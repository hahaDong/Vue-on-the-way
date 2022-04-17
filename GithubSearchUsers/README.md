# GithubSearchUsers
用户在输入框中输入有效内容并点击搜索按钮，程序会将查询到的相关结果渲染在列表中。

# 功能模块
+ 使用axios发送ajax请求

# 效果图

<div align="center">
  <img src="https://user-images.githubusercontent.com/41555864/163710111-12bb242c-e5ab-49bc-beb5-8b5f5ec40f3a.png">
  <span>未发送请求</span>
</div>
<hr/>
<div align="center">
  <img src="https://user-images.githubusercontent.com/41555864/163710153-a2edd06b-600d-486a-a17e-382e25f0ebe3.png">
  <span>已发送请求但未收到响应</span>
</div>
<hr/>
<div align="center">
  <img src="https://user-images.githubusercontent.com/41555864/163707380-01153fdb-c744-4428-9f33-9ddb240c74dc.png">
  <span>请求成功</span>
</div>
<hr/>
<div align="center">
  <img src="https://user-images.githubusercontent.com/41555864/163710174-1b26ed98-aade-455a-87fe-4d851674905b.png">
  <span>请求失败</span>
</div>
<hr/>

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
