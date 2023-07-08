## MatterMost协议分析

### 认证

我们已经有一个用户peter，口令是Welcome2023。

你使用著名的curl工具对MatterMost的协议进行分析。在命令行上运行curl
```
$ curl -i -d '{"login_id":"peter","password":"Welcome2023"}' https://im.wochat.org/api/v4/users/login
HTTP/1.1 200 OK
Content-Type: application/json
Permissions-Policy: 
Referrer-Policy: no-referrer
Token: wozb59cxejf9ugj9ieg8eueoge         <----------- Token
Vary: Accept-Encoding
X-Content-Type-Options: nosniff
X-Request-Id: wrfcxxqoqfd5tc7s7t686rr7hr
X-Version-Id: 7.10.3.7.10.3.8ab39ba0e463c8ad270eda47588aab20.false
Date: Sat, 08 Jul 2023 13:12:40 GMT
Content-Length: 699

{"id":"r6xpx19wu7g1bqcbgzbd1mbdpr","create_at":1688820874520,"update_at":1688820901321,"delete_at":0,"username":"peter","auth_data":"","auth_service":"","email":"peter@peter.com","nickname":"","first_name":"","last_name":"","position":"","roles":"system_user","notify_props":{"channel":"true","comments":"never","desktop":"mention","desktop_sound":"true","desktop_threads":"all","email":"true","email_threads":"all","first_name":"false","mention_keys":"","push":"mention","push_status":"away","push_threads":"all"},"last_password_update":1688820874520,"locale":"en","timezone":{"automaticTimezone":"America/New_York","manualTimezone":"","useAutomaticTimezone":"true"},"disable_welcome_email":false}
```
我们可以看到，服务器端返回一个Token。此后的API调用均使用这个Token和服务器进行交互。在这个Token有效期内，服务器认为该用户均在已经登录的状态了。
参考官方文档：
https://api.mattermost.com/#tag/authentication

