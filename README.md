# Auto-SSL

----
# Warning!!!看下面👇！！！ 
## 一定要新建个private repo，然后把这里的代码 push 到你自己的 github private repo,不然Cert的私钥就泄露了
----

## Introduction
这是一个使用 GitHub Actions 通过 acme.sh 自动申请 SSL 证书的项目。

## Features
- 自动申请SSL 证书,并通过 git commit 的方式保存证书到 SSL
- 每天检查SSL 证书是否快过期，如果小于30天，自动续期
- 每天的检查报告会同步到 CHECK_LIST.md 文件中
- 证书是泛域名证书
- 同时申请 ECDSA 和 RSA 证书

## How to use
### 1. 申请域名

确保已经拥有一个域名。如果没有，您可以通过各大域名注册商申请。

### 2. 域名托管到 Cloudflare

将您的域名托管到 Cloudflare 上。这一步骤确保了您可以通过 Cloudflare 管理您的 DNS 记录。

### 3. 申请 Cloudflare 的 API Token
非Cloudflare参见 
https://github.com/danbao/auto-ssl/issues/3 
https://github.com/acmesh-official/acme.sh/wiki/dnsapi

访问 Cloudflare 的 API Token 管理页面，申请一个 API Token。

CF_Token 可以在这里申请 https://dash.cloudflare.com/profile/api-tokens, 权限需要Edit zone DNS

<img width="1045" alt="image" src="https://github.com/danbao/auto-ssl/assets/4090783/ea014646-8cbe-4064-a764-b45281e42e55">

CF_Account_ID 点开Cloudflare首页，随便点击一个你托管在此的域名，在右侧会显示CF_Account_ID。

<img width="443" alt="image" src="https://github.com/danbao/auto-ssl/assets/4090783/d1d86260-89ce-4179-a0c2-e8a2361e627f">

### 4. 配置 GitHub 仓库的 Secrets

在您的 GitHub 仓库中，依次访问 `Settings -> Security -> Secrets and variables -> Actions`，添加以下三个变量：
- `CF_TOKEN`：在上一步中获取的 Cloudflare API Token。
- `CF_ACCOUNT_ID`：在上一步中获取的 Cloudflare Account ID。
- `EMAIL`：申请SSL需要的邮箱地址。

<img width="1177" alt="image" src="https://github.com/danbao/auto-ssl/assets/4090783/e3ea47d8-7b3e-4605-94ee-689e6bb6ca45">

### 5. 设置 GitHub Actions 权限

在 GitHub 仓库中，依次访问 `Settings -> Code and automation -> Actions -> General -> Workflow permissions`，勾选 `Read and write permissions` 权限。

<img width="827" alt="image" src="https://github.com/danbao/auto-ssl/assets/4090783/abb42eb0-fd78-4417-bf07-9cf090ee7a2c">

### 6. 修改 repo 中的 cloudflare_domains_list.txt
把里面的域名改为你自己的域名，可以填多个域名每行一个

### 8. 手动触发 GitHub Actions
