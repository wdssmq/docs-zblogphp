## member 会员登录及管理 API

| act 方法 | 请求方式   | 参数                                                | 鉴权 |
| -------- | ---------- | --------------------------------------------------- | ---- |
| `login`  | POST       |`用户登录并返回 token`                                 |      |
|          |            |$_POST['username'] 用户名称(非别名)
|          |            |$_POST['password']`password`建议使用 MD5(明文密码) 值
|          |            |$_POST['savedate'] `token`过期时间，最长 365 天
|          |            |返回值：附：**「示例 1」**
|
| `post`   | POST       | `编辑用户或新建用户`                                    | 必须 |
|          |            | `Member`定义字段；附：**「示例 2」**
|
| `get`    | GET / POST | `获取一个用户信息`                                         | 必须 |
|          |            | $_REQUEST['id'] 用户 `id`
|
| `delete` | GET / POST | `删除一个用户`                                           | 必须 |
|          |            | $_REQUEST['id'] 用户 `id`
|
| `list`   | GET / POST | `获取用户管理列表`                                       | 必须 |
|          |            | `act=list`方法共通参数见：[约束与过滤](books/api-05-design?id=约束与过滤 "约束与过滤")
|          |            | $_REQUEST['status'] 指定状态`status`
|          |            | $_REQUEST['level'] 指定用户`level`
|          |            | $_REQUEST['page'] 第几页'page'
|
|`get_auth`| GET / POST | `查看当前用户权限列表`                                  | 必须 |
|
|`logout`| GET / POST | `退出登录`                                                | 必须 |
|          |            | PS:然后客户端自行删除 token 即可
|



**示例 1**：

<details>
<summary>login 登录成功后返回值：（点击展开）</summary>

```php
//发送的POST字段如下
username = '用户名'
password = md5('密码明文')
savedate = '保存天数'
```

```json
{
    "code": 200,
    "message": "操作成功",
    "data": {
        "user": {
            "ID": "1",
            "Level": "1",
            "Status": "0",
            "Name": "admin",
            "StaticName": "admin" // 等等 members 相关信息
        },
        "token": "Token 信息",
        "expire_time": 1672560322 // 过期时间
    },
    "error": null,
    "runtime": {
    }
}
```
此处`login`操作返回的「鉴权 Token」将用于后续需要「鉴权」的请求，见「[权限认证](books/api-05-design?id=权限认证 "权限认证")」；
</details>

**示例 2**：

<details>
<summary>post 创建一个用户：（点击展开）</summary>

```json
{
  "ID": "0",
  "Level": "4",
  "Name": "用户名",
  "Password": "zblog_pwdd",
  "PasswordRe": "zblog_pwdd"
}
```

`"ID": "0",` 必须显示设置；

`"Level": "4",` 为用户等级；参考「[用户等级划定](books/start-25-faq?id=用户等级划定 "用户等级划定")」
</details>




