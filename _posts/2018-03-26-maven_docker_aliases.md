---
title: Adding tags to docker-maven-plugin
layout: post
category:
date: 2018-03-26 12:36:42 BST
tags:
  - containers
  - maven
published: true
---

Adding a ``latest`` tag to docker containers built by [docker-maven-plugin](https://github.com/fabric8io/docker-maven-plugin)
```
  <name>${project.artifactId}:${project.version}</name>
  <build>
      <tags combine.children="append">
        <tag>latest</tag>
      </tags>
      <from>${base.docker.image}</from>
```
