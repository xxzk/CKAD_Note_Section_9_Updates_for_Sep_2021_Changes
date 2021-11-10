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

