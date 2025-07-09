# auth-service

负责用户账号、权限和 API Token 管理。提供以下主要功能：

- 用户注册、登录、找回密码
- 角色与权限配置
- OAuth/OpenID 等第三方登录集成
- API Key 签发与校验

其它服务通过验证 Token 或调用用户信息接口进行授权。
