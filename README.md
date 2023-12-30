# nezha-serv

用到的变量
  | 变量名        | 是否必须  | 备注 |
  | ------------ | ------   | ---- |
  | GH_USER             | 是 | github 的用户名，用于面板管理授权 |
  | GH_CLIENTID         | 是 | 在 github 上申请 |
  | GH_CLIENTSECRET     | 是 | 在 github 上申请 |
  | GH_BACKUP_USER      | 否 | 在 github 上备份哪吒服务端数据库的 github 用户名，不填则与面板管理授权的账户 GH_USER 一致  |
  | GH_REPO             | 否 | 在 github 上备份哪吒服务端数据库文件的 github 库 |
  | GH_EMAIL            | 否 | github 的邮箱，用于备份的 git 推送到远程库 |
  | GH_PAT              | 否 | github 的 PAT |
  | REVERSE_PROXY_MODE  | 否 | 默认使用 Caddy 应用来反代，这时可以不填写该变量；如需 Nginx 或 gRPCwebProxy 反代，请设置该值为 `nginx ` 或 `grpcwebproxy` |
  | ARGO_AUTH           | 是 | Json: 从 https://fscarmen.cloudflare.now.cc 获取的 Argo Json<br> Token: 从 Cloudflare 官网获取 |
  | ARGO_DOMAIN         | 是 | Argo 域名 |
  | NO_AUTO_RENEW       | 否 | 默认不需要该变量，即每天定时同步在线最新的备份和还原脚本。如不需要该功能，设置此变量，并赋值为 `1` | 
