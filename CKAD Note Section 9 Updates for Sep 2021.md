# CKAD Note Section 9 Updates for Sep 2021 Changes

<br>

![CKAD_20210928_change](CKAD_20210928_change.jpg)

▲ CKAD 新舊版差異

<br>

## 119. Define, build and modify container images

<br>

非常基礎的 Docker Image (container image) 介紹，我之前就打過一篇在公司 Bookstack 了~\
《Docker Image 介紹》

<br>

## 121. Authentication, Authorization and Admission Control

<br>

除了 master,worker node 本身的安全機制 (例如: SSH public key ONLY) 以外\
`kube-apiserver` 在 K8s cluster 當中扮演非常關鍵的角色必須要被嚴格控管，接下來的章節會介紹 How to\
一開始我們先來探討一下 **Who can access?** 與 **What can they do?**

<br>

### Who can access?


<br>

![who_can_access](who_can_access.jpg)


- Files - username and passwds
- Files - username and tokens
- Certification
- 外部授權平台 (例如: LDAP)
- Service Account

<br>

### What can they do?


~~其實我不知道中文怎麼翻.. What can they do ??~~  總之看起來像 K8s 的授權 (Authorization) 控管方式:


- RBAC Authorization. (Role Base Access Control)
- ABAC Authorization. (Attribute Base Access Control)
- Webhook Mode

<br>

![tls_certs](tls_certs.jpg)

▲ K8s cluster 內各個元件在溝通時都透過 TLS 加密

<br>

## 122. Authentication

<br>

本章節的重點會放在三種不同 user 如何透過 Authentication 機制安全的訪問 K8s cluster


- K8s cluster admin
- Developer
- ~~End User~~ (在這邊被移除，講師認為 sercurity 責任應該在 app 本身)
- Bots (service account)

<br>

![k8s_account_0](k8s_account_0.jpg)

▲ Kubernetes cluster 原始狀態並沒有提供使用者的功能

<br>

![k8s_account_1](k8s_account_1.jpg)

▲ 不管是透過 `kubectl` 或者 `curl` (不知道是不是就是在說 Dashboard) 都要找 `kube-apiserver`。首先會 (1) Authenticate Users (2) Process request。

<br>

![k8s_account_2](k8s_account_2.jpg)

驗證 (authentication) 的方式有這些:

- Static Password File
- Static Token File
- Certificates
- External service (EX: LDAP)

<br>

### File

前兩項都是以 file 的形式去給定使用者帳號跟密碼。 **<span style='color:red'>兩種都不建議使用</span>**


```csv
## <passwd>,<username>,<user_id>,<group_name>
password123,user1,u0001
```

<br>

![k8s_account_3](k8s_account_3.jpg)

▲ 然後在啟動 `kube-apiserver` 的時候傳進去

<br>

![k8s_account_4](k8s_account_4.jpg)

▲ `curl` 搭配 user/passwd 的認證方式

<br>

![k8s_account_5](k8s_account_5.jpg)

▲ `token` 的部分

<br>

