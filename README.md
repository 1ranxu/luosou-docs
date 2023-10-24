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
- URL记录页面搜索状态
- 整合Axios
- 文章列表页面
- 用户列表页面

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

3. 引入组件库

```sh
npm i --save ant-design-vue@4.x
```

![image-20231022192910316](assets/image-20231022192910316.png)

![image-20231022193631491](assets/image-20231022193631491.png)

![image-20231022194135553](assets/image-20231022194135553.png)

![image-20231022194239266](assets/image-20231022194239266.png)

4. 启动

![image-20231022194521264](assets/image-20231022194521264.png)

![image-20231022194543465](assets/image-20231022194543465.png)

### 后端

1. 使用模板 

   把模板的目录名改成项目名

2. 连接本地数据库

3. 创建数据库

![image-20231024105038607](assets/image-20231024105038607.png)

![image-20231024105146892](assets/image-20231024105146892.png)

![image-20231024105529958](assets/image-20231024105529958.png)

4. 开启redis

![image-20231024110212959](assets/image-20231024110212959.png)

![image-20231024110048308](assets/image-20231024110048308.png)

5. 修改端口

![image-20231024110522118](assets/image-20231024110522118.png)

6. 修改项目名

![image-20231024111455584](assets/image-20231024111455584.png)

![image-20231024111615892](assets/image-20231024111615892.png)

7. 启动并访问接口文档



## 前端

### 搜索页面

1. 修整文件

![image-20231024135928686](assets/image-20231024135928686.png)

![image-20231024141918918](assets/image-20231024141918918.png)

![image-20231024141945652](assets/image-20231024141945652.png)

![image-20231024150433167](assets/image-20231024150433167.png)

2. 选择组件

![image-20231024143606700](assets/image-20231024143606700.png)

![image-20231024143754447](assets/image-20231024143754447.png)

3. 引入组件

![image-20231024144828443](assets/image-20231024144828443.png)

![image-20231024144744726](assets/image-20231024144744726.png)

![image-20231024150050490](assets/image-20231024150050490.png)

![image-20231024153210062](assets/image-20231024153210062.png)

![image-20231024145457465](assets/image-20231024145457465.png)

![image-20231024150119730](assets/image-20231024150119730.png)

![image-20231024150204097](assets/image-20231024150204097.png)

4. 美化页面

![image-20231024151930960](assets/image-20231024151930960.png)

![image-20231024153031899](assets/image-20231024153031899.png)

![image-20231024153123088](assets/image-20231024153123088.png)

![image-20231024155542929](assets/image-20231024155542929.png)

5. 展示



### URL记录页面搜索状态

用URL记录页面搜索状态，当用户刷新页面时，能够从URL还原之前的页面搜索状态

**核心：**

状态同步改为单向，即只允许URL来改变页面状态，不允许反向

1. 用户与页面交互时，改变URL地址（例如：点击搜索，需要把搜索内容填充的URL；切换Tab时，URL也要填充tab）
2. 当URL地址改变时，改变页面状态（监听URL的变化）

**实现：**

1. 添加动态路由

![image-20231024163914930](assets/image-20231024163914930.png)

2. 用户与页面交互时，改变URL地址

![image-20231024164652907](assets/image-20231024164652907.png)

![image-20231024164738185](assets/image-20231024164738185.png)

3. 当URL地址改变时，改变页面状态

![image-20231024165059112](assets/image-20231024165059112.png)

![image-20231024165206867](assets/image-20231024165206867.png)

### 整合Axios

[起步 | Axios中文文档 | Axios中文网 (axios-http.cn)](https://www.axios-http.cn/docs/intro)

1. 安装

```sh
npm install axios
```

![image-20231024172207470](assets/image-20231024172207470.png)

2. 创建实例

```ts
import axios from "axios";

const myAxios = axios.create({
  baseURL: "http://localhost:8083/api",
  timeout: 10000,
});
myAxios.defaults.withCredentials = true;

// 添加请求拦截器
myAxios.interceptors.request.use(
  function (config) {
    // 在发送请求之前做些什么
    return config;
  },
  function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  }
);

// 添加响应拦截器
myAxios.interceptors.response.use(
  function (response) {
    // 2xx 范围内的状态码都会触发该函数。
    // 对响应数据做点什么
    const data = response.data;
    if (data.code === 0) {
      return data.data;
    } else {
      throw new Error(data.message);
    }
  },
  function (error) {
    // 超出 2xx 范围的状态码都会触发该函数。
    // 对响应错误做点什么
    return Promise.reject(error);
  }
);

export default myAxios;
```

### 文章列表页面

1. 选择组件

![image-20231024173720714](assets/image-20231024173720714.png)

2. 引入组件

![image-20231024173758369](assets/image-20231024173758369.png)

![image-20231024181656555](assets/image-20231024181656555.png)

![image-20231024181713307](assets/image-20231024181713307.png)

![image-20231024181904943](assets/image-20231024181904943.png)

3. 展示

![image-20231024181816312](assets/image-20231024181816312.png)

### 用户列表页面

1. 选择组件

![image-20231024182216882](assets/image-20231024182216882.png)

2. 引入组件

   先把文章列表页面复制过来，post全局替换成user

![image-20231024192333227](assets/image-20231024192333227.png)

![image-20231024192406747](assets/image-20231024192406747.png)

![image-20231024192418009](assets/image-20231024192418009.png)

## 后端

### 基本搜索接口