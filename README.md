# nezha-serv

加强备份恢复逻辑，保证不丢失数据：

1、24小时强制备份

2、每分钟检查配置变化，发现新本容即立即备份

3、每分钟检查配置变化，发现文件重置立即恢复最新备份

4、每次重启自动恢复最新备份

5、使用同一个备份库同一配置即可任意搬迁项目到任何容器

6、每24小时自动检测面板程序版本，发现新版本自动更新，无需重新部署


## 准备需要用的变量
* 到 Cloudflare 官网，选择使用的域名，打开 `网络` 选项将 `gRPC` 开关打开

<img width="1590" alt="image" src="https://user-images.githubusercontent.com/92626977/233138703-faab8596-a64a-40bb-afe6-52711489fbcf.png">

* 获取 github 认证授权: https://github.com/settings/applications/new

面板域名加上 `https://` 开头，回调地址再加上 `/oauth2/callback` 结尾

<img width="916" alt="image" src="https://user-images.githubusercontent.com/92626977/231099071-b6676f2f-6c7b-4e2f-8411-c134143cab24.png">
<img width="1122" alt="image" src="https://user-images.githubusercontent.com/92626977/231086319-1b625dc6-713b-4a62-80b1-cc5b2b7ef3ca.png">

* 获取 github 的 PAT (Personal Access Token): https://github.com/settings/tokens/new

<img width="1226" alt="image" src="https://user-images.githubusercontent.com/92626977/233346036-60819f98-c89a-4cef-b134-0d47c5cc333d.png">
<img width="1148" alt="image" src="https://user-images.githubusercontent.com/92626977/233346508-273c422e-05c3-4c91-9fae-438202364787.png">

* 创建 github 用于备份的私库: https://github.com/new

<img width="814" alt="image" src="https://user-images.githubusercontent.com/92626977/233345537-c5b9dc27-35c4-407b-8809-b0ef68d9ad55.png">

用到的变量
  | 变量名        | 是否必须  | 备注 |
  | ------------ | ------   | ---- |
  | GH_USER             | 是 | github 的用户名，用于面板管理授权 |
  | GH_CLIENTID         | 是 | 在 github 上申请 |
  | GH_CLIENTSECRET     | 是 | 在 github 上申请 |
  | GH_REPO             | 否 | 在 github 上备份哪吒服务端数据库文件的 github 库 |
  | EMAIL               | 否 | github 的邮箱，用于备份的 git 推送到远程库 |
  | GH_PAT              | 否 | github 的 PAT |
  | TOK                 | 是 | 隧道的TOKEN|
  | ARGO_DOMAIN         | 是 | Argo 域名 |
  | BEIFEN_TIME         | 否 | 强制备份间隔，分钟为单位，默认1440表示24小时 |
  | PORT                | 否 |默认7860 |
  | PSWD               | 是 |启动密码 |

