---
title: "Thoughts on Kubernetes"
layout: post
category:
date: 2017-01-27 19:36:42 BST
tags:
  - containers
  - kubernetes
published: true
---

Just a collection of annoyances on Kubernetes:

# kubectl config and multiple namespaces

_Seriously!_ The shear amount of YAML duplication if you have a large
number of namespaces and clusters it quite rapidly becomes very annoying,
do remember that this is YAML so you could have (ab)used anchors to copy
commonly used fragments:

```yaml
    apiVersion: v1
    clusters:
    - cluster:
        server: https://cluster1.example.com
      name: cluster1
    contexts:
    - context: &bar-ns
        cluster: cluster1
        namespace: bar-namespace
        user: "cluster1-user"
      name: cluster1-bar-namespace
    - context:
        <<: *bar-ns
        namespace: foo-namespace
      name: cluster1-foo-namespace
    - context:
        <<: *bar-ns
        namespace: kube-system
      name: cluster1-kubesystem
    current-context: cluster1-foo-namespace
    kind: Config
    preferences: {}
    users: []
```

```bash
CURRENT   NAME                     CLUSTER    AUTHINFO   NAMESPACE
*         cluster1-foo-namespace   cluster1              foo-namespace
          cluster1-kubesystem      cluster1              kube-system
          cluster1-bar-namespace   cluster1              bar-namespace
```

_Except:_ as soon as you use ``kubectl config use-context`` it goes and
helpfully writes back the expanded YAML structure. This makes sense but is
remarkably unhelpful as it goes.

You can of course template a number of ~/.kube/CONFIG_FILES and then use the following to switch:

```bash
$ export KUBECONFIG=~/.kube/config-a
$ kubectl get pods
```

# Documentation

Maybe it's the rapid pace of change within the software, but it's full of
holes, and yes I should raise pull requests for changes to the documentation,
but look at the [CentOS instructions](https://kubernetes.io/docs/getting-started-guides/centos/centos_manual_config/)

Where the repo contains packages for Kubernetes 1.1.0 - from 2015!

# DNS

Headless services without selectors are very helpful, but unfortunately a TTL of 30 seconds that is currently fixed can be limiting.
