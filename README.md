# 哪吒面板nodejs重写版

加强备份恢复逻辑，保证在不稳定的环境下不丢失数据：

1、24小时强制备份

2、每3分钟检查配置变化，发现变化立即备份

3、每3分钟检查配置变化，发现配置重置立即恢复最新备份

4、每次重启自动恢复最新备份

5、使用同一个备份库同一配置即可任意搬迁项目到任何容器

6、每24小时自动检测面板程序版本，发现新版本自动更新，无需重新部署


## 支持一键换哪吒面板配置
在备份仓库创建文件env.json，格式如下:
```
{
  "TOK": "your_token_value",
  "ARGO_DOMAIN": "your_argo_domain_value",
  "GH_CLIENTID": "your_github_client_id_value",
  "GH_CLIENTSECRET": "your_github_client_secret_value",
}
```
然后查看日志一键命令，浏览器输入命令即可一键替换新的面板配置

小技巧：可以把一键命令放入备份仓库的read.me，点击即可备份恢复,比如：
```
哪吒服务器的一键备份 https://xxxx.com/benfen-xxx

哪吒服务器的一键恢复 https://xxxx.com/huifu-xxx

哪吒服务器的一键更换 https://xxxx.com/genghuan-xxx

哪吒服务器的一键部署 https://api.xxxx.com/deploy
```
## F大教程，注意不要照搬，看下面参数设置，端口有所改变

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

### (部署方式 - Token): 通过 Cloudflare 官网，手动生成 Argo 隧道 token 信息
#### 到 cf 官网：https://dash.cloudflare.com/
* 进入 zero trust 里生成 token 隧道和信息。
* 其中数据路径 443/https 为 `proto.NezhaService`
* ssh 路径 22/ssh 为 < client id >

<img width="1672" alt="image" src="https://github.com/fscarmen2/Argo-Nezha-Service-Container/assets/92626977/0c467d8b-5fbc-4bde-ac8a-db70ed8798f0">
<img width="1659" alt="image" src="https://github.com/fscarmen2/Argo-Nezha-Service-Container/assets/92626977/5aa4df19-f277-4582-8a4d-eef34a00085c">
<img width="1470" alt="image" src="https://github.com/fscarmen2/Argo-Nezha-Service-Container/assets/92626977/ec06ec20-a68d-405c-b6de-cd4c52cbd8c0">
<img width="1342" alt="image" src="https://github.com/fscarmen2/Argo-Nezha-Service-Container/assets/92626977/538707e1-a17b-4a0f-a8c0-63d0c7bc96aa">
<img width="1020" alt="image" src="https://github.com/fscarmen2/Argo-Nezha-Service-Container/assets/92626977/9f5778fd-aa94-4fda-9d85-552b68f6d530">
<img width="1652" alt="image" src="https://github.com/fscarmen2/Argo-Nezha-Service-Container/assets/92626977/d0fba15c-f41b-4ee4-bea3-f0506d9b2d23">
<img width="1410" alt="image" src="https://github.com/fscarmen2/Argo-Nezha-Service-Container/assets/92626977/228b8e86-32a8-479a-8a86-89ed9b8b5b5e">


##      变量参考
  | 变量名        | 是否必须  | 备注 |
  | ------------ | ------   | ---- |
  | GH_USER             | 是 | github 的用户名，用于面板管理授权 |
  | GH_CLIENTID         | 是 | 在 github 上申请 |
  | GH_CLIENTSECRET     | 是 | 在 github 上申请 |
  | GH_REPO             | 否 | 在 github 上备份哪吒服务端数据库文件的 github 库 |
  | EMAIL               | 否 | github 的邮箱，用于备份的 git 推送到远程库 |
  | GH_PAT              | 否 | github 的 PAT |
  | TOK                 | 是 | 隧道的TOKEN|
  | WANGZHI         | 是 | Argo 域名 |
  | BEIFEN_TIME         | 否 | 强制备份间隔，分钟为单位，默认1440表示24小时 |
  | PORT                | 否 |默认7860 |
  | WEB_PORT            | 否 |默认8080，即隧道设置为http的端口，为面板web管理端口 |
  | ROXY_PORT     | 否 |默认8443，即隧道设置为https的端口，为面板数据通信端口 |
  | PSWD                | 是 |启动密码 |



附：F大佬原版地址：https://github.com/fscarmen2/Argo-Nezha-Service-Container.git



# 免责声明:

本仓库仅为自用备份，非开源项目，因为需要外链必须公开，但是任何人不得私自下载, 如果下载了，请于下载后 24 小时内删除, 不得用作任何商业用途, 文字、数据及图片均有所属版权。 

如果你使用本仓库文件，造成的任何责任与本人无关, 本人不对使用者任何不当行为负责。

