# 幻腾Oauth认证接入指南

### 注册第三方应用
首先，开发者必须拥有一个有效的幻腾帐号，如果您还没有的话，请先[注册](https://huantengsmart.com/users/sign_up)。
然后，访问[这里](https://huantengsmart.com/oauth2/applications)注册一个第三方应用。

  * Name：填写中文英文都可以
  * Redirect URI：填写接收`authorize_code`的回调地址
  * Scopes：填写需要的权限。如需多个权限，请用 **半角空格** 分隔。目前可用的权限有：
    * public
    * pixel_pro
    * door_accessor
    * bulb
    * user

应用创建成功后，您会得到 **Application Id** 和 **Secret**。
务必妥善保管，不要外泄。


### 请求用户授权
请用 **GET** 方法访问： [https://huantengsmart.com/oauth2/authorize](https://huantengsmart.com/oauth2/authorize)

并提供如下参数：

  * client_id：在上一个步骤中获取
  * redirect_uri：一定要用 urlencode 编码
  * response_type：填写 `code`
  * scope：多个权限之间用 `+` 连接

使用户被导航到这个页面，用户会被要求登录，登录成功后会显示一个页面询问用户是否同意您的程序使用该用户的数据。
如果用户选择同意，那么系统会把 `authorize code` 以如下方式发送到您填写的 `redirect_uri`：

```
GET redirect_uri/?code=authorize_code
```

如果用户选择拒绝，那么系统会这样通知您：

```
GET redirect_uri/?error=access_denied&error_description=The+resource+owner+or+authorization+server+denied+the+request.
```

**注意： `authorize code` 的有效期只有10分钟，请在有效期内完成换取 Access Token 的操作**

curl 示例

```
curl -X GET https://huantengsmart.com/oauth2/authorize?\
client_id=700e2f045584698603bdb92a6b6d5fce9eadd772c4555012121000c8938e2301&\
redirect_uri=urn:ietf:wg:oauth:2.0:oob&\
response_type=code&\
scope=read_user+write_user+monitor_user
```


### 换取 Access Token
请用 **POST** 方法访问：[https://huantengsmart.com/oauth2/token](https://huantengsmart.com/oauth2/token)

并提供如下参数：

  * client_id：在第一步中获取
  * client_secret：在第一步中获取
  * redirect_uri：一定要用 urlencode 编码
  * grant_type: 填写 `authorization_code`
  * code：在请求用户授权时获取的 `authorize code`

如果所有参数都正确的话，您会获取到 `access_token`:

```
{
    "access_token": "98189af6ab0c2fe2cd85f6add64d7410a3c04265340376afea8ee1e014dfd310",
    "token_type": "bearer",
    "expires_in": 2592000,
    "refresh_token": "a4374171ffe63cf1ae34204ec885cf7bce23699e299c95b2c4e1363731fe2976",
    "scope": "public",
    "created_at": 1454294827
}
```

如果有任一参数错误，您会得到如下错误信息：

```
{
    "error": "invalid_grant",
    "error_description": "The provided authorization grant is invalid, expired, revoked, does not match the redirection URI used in the authorization request, or was issued to another client."
}
```

**注意： `access_token` 的有效期是30天**

curl示例

```
curl -X POST --form client_id=700e2f045584698603bdb92a6b6d5fce9eadd772c4555012121000c8938e2301 \
--form client_secret=397acfb8065b1f885958356acd0a98fe77115bdaaebf24c4a7ecd275380e8830 \
--form redirect_uri=urn:ietf:wg:oauth:2.0:oob \
--form grant_type=authorization_code \
--form code=9eeaa04ed7dd538840e17bef0e9bea2dddc928ec14f288cb03d5842cb2aa8e8c \
https://huantengsmart.com/oauth2/token

```


### 使用 Access Token （鉴权）
在访问任一幻腾 Api 时，在 Http 请求的头部加入：
```
Authorization: bearer access_token
```

**注意： 单词 `bearer` 必须小写**

如果令牌有效，那么您会正常获取到 Api 返回的数据；否则您会得到 401 错误。

curl示例

```
curl -X GET --header "Authorization: bearer 26c115b6be971cfdd11297a00697e200fa011a959ca0fa8582fdf4b36108f6f2" \
--header "Accept: application/json" \
https://huantengsmart.com/api/bulb.json
```


### 刷新 Access Token
如果遇到 `access_token` 过期的场景，您可以这样直接获取新的 `access_token`，而无需再次征得用户的授权。

请用 **POST** 方法访问：[https://huantengsmart.com/oauth2/token](https://huantengsmart.com/oauth2/token)

并提供如下参数：

  * grant_type：填写 `refresh_token`
  * refresh_token： 在换取 Access Token 时获取的 `refresh_token`

如果参数都正确，您会得到一组新的令牌。

**注意：此接口需鉴权**

**提示：最好在每一次访问 Api 之前都判断 `access_token` 是否过期**

curl示例

```
curl -X POST --header "Authorization: bearer 26c115b6be971cfdd11297a00697e200fa011a959ca0fa8582fdf4b36108f6f2" \
--header "Accept: application/json" \
--form grant_type=refresh_token \
--form refresh_token=d216c76ce5e9a8fd56f019b2683521ca24ae7a66bdf707b427e36b88f2a1bd3e \
https://huantengsmart.com/oauth2/token
```


### 销毁 Access Token
请用 **POST** 方法访问：[https://huantengsmart.com/oauth2/revoke](https://huantengsmart.com/oauth2/revoke)

并提供如下参数：

  * token: 在换取 Access Token 时获取的 `access_token`

无论成功或失败，服务器都会返回一个空的 JSON 对象，且 http status code 是 200。
所以，**不要** 用此接口的返回值作为任何逻辑判断的依据。

**注意：此接口需鉴权**

curl示例

```
curl -X POST --header "Authorization: bearer 9b60ce452d1360b5ca734a28faf76b6a4b2eb921551ee6f8c836afca6120eca1" \
--header "Accept: application/json" \
--form token=9b60ce452d1360b5ca734a28faf76b6a4b2eb921551ee6f8c836afca6120eca1 \
https://huantengsmart.com/oauth2/revoke
```
