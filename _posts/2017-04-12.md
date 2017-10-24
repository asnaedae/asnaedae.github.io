---
title: starting kubernetes
layout: post
category:
date: 2017-04-12 16:36:42 BST
tags:
  - containers
  - kubernetes
published: true
---

Getting kubernetes to start with RBAC features enabled

```bash
$ minikube start --vm-driver=xhyve \
	--extra-config=apiserver.GenericServerRunOptions.AuthorizationMode=RBAC,--authorization-rbac-super-user=minikube-admin \
	--kubernetes-version=v1.6.0 --memory=4096 --cpus 4
```

