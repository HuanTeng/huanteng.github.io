# 幻腾推送服务接入说明

## 步骤

### 0. 注册幻腾账号
第三方开发者首先要注册一个幻腾账号。
[https://huantengsmart.com/users/sign_up](https://huantengsmart.com/users/sign_up)


![注册页面](https://github.com/HuanTeng/huanteng.github.io/blob/master/images/oauth/0_注册.jpeg)

### 1. 登录幻腾账号
[https://huantengsmart.com/users/sign_in](https://huantengsmart.com/users/sign_in)


![登录页面](https://github.com/HuanTeng/huanteng.github.io/blob/master/images/oauth/1_登录.jpeg "登录")

### 2. 新建应用
[https://huantengsmart.com/oauth2/applications](https://huantengsmart.com/oauth2/applications)


![应用管理页](https://github.com/HuanTeng/huanteng.github.io/blob/master/images/oauth/2_app管理界面.jpeg "应用管理页")


点击"New Application"进入注册页面


![应用注册页](https://github.com/HuanTeng/huanteng.github.io/blob/master/images/oauth/3_新建app.jpeg "新建应用")


* **Name** 应用的名称
* **Redirect URI** 接收 code 和 access_token 的地址
* **Scopes** 按照需求勾选
* **Notification url** 用来接收 Monitor Scopes 的通知。必须以 http:// 开头。
点击 Submit 创建应用。

### 3. 查看新建应用
![应用详情页](https://github.com/HuanTeng/huanteng.github.io/blob/master/images/oauth/4_app详情.jpeg "应用详情")


**注意：请妥善保存该页的信息。**

### 4. 使用OAuth
请看[幻腾OAuth认证接入指南](https://github.com/HuanTeng/huanteng.github.io/blob/master/oauth.md)
