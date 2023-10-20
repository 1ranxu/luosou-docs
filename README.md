# 落樱搜索

## 项目介绍

用户可以在同一个入口（同一个页面）集中搜索出不同来源，不同类型的内容

**对于用户：**

- 提升用户的检索效率，提升用户的体验

**对于企业：**

- 无需针对每一个项目都去开发一个搜索功能，当你有新内容，新网站时，复用同一套搜索系统，提升开发效率

## 技术选型

**前端：**

- Vue
- Ant Design Vue
- Lodash

**后端：**

- Spring Boot
- MySQL
- ElasticSearch（Elastic Stack）搜索引擎
- 数据抓取
  - 离线
  - 实时
- 数据同步
  - 定时
  - 双写
  - logstash
  - Canal
- Guava Retrying
- Jmeter

## 业务流程

1. 先得到各种不同分类的数据
2. 提供一个搜索页面（单一搜索 + 聚合搜索），支持搜索
3. 单一搜索：根据关键词只搜索某个分类下的内容
4. 聚合搜索：根据关键词搜索不同分类下的内容

![image-20231019220250243](assets/image-20231019220250243.png)

## 计划

**初始化**

- 前端
- 后端

**前端**

- 搜索页面

**后端**

- 基本搜索接口
- 数据抓取
- 聚合搜搜接口
  - 适配器模式
  - 门面模式
- ElasticSearch的搭建及入门
- ElasticSearch的使用（建表，读写数据，调API，整合）
- 数据同步

**优化**

- 保障接口稳定性

- 搜索结果关键词高亮
- 搜索建议提示
- 防抖节流

## 初始化

### 前端

[快速上手 - Ant Design Vue (antdv.com)](https://antdv.com/docs/vue/getting-started-cn)

1. 安装脚手架工具[vue-cli](https://github.com/vuejs/vue-cli)

```sh
#权限不够，就以管理员身份打开CMD
npm install -g @vue/cli
```

![image-20231020142533775](assets/image-20231020142533775.png)

2. 创建一个项目

```sh
vue create luosou-frontend
```

![image-20231020143053401](assets/image-20231020143053401.png)

![image-20231020143308813](assets/image-20231020143308813.png)

![image-20231020143355434](assets/image-20231020143355434.png)

![image-20231020143606033](assets/image-20231020143606033.png)

![image-20231020143905644](assets/image-20231020143905644.png)

### 后端

## 前端

### 搜索页面



## 后端

### 基本搜索接口