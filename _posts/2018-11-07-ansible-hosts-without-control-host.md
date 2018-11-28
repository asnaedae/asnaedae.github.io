---
title: Ansible hosts and groups when not using a control host
layout: post
category:
date: 2018-11-07 12:36:42 BST
tags:
  - ansible
  - random
published: true
---

Had a client with a deployment tool that would copy a bundle of Ansible to each host and run  ansible-playbook locally on each host defined. This had some interesting side effects where you want to the same play on multiple hosts

E.g.

```
[webservers]
host1.domain.net ansible_connection=local
host2.domain.net ansible_connection=local
```

Normally this would force all members of the webservers group to be run locally, so used the following little block:

```
- hosts: webservers

  tasks:
    - name: foo
      debug:
        msg: "test message for {{ ansible_hostname }} - {{ ansible_fqdn }} - {{ ansible_host }}"
      when: ansible_host == ansible_hostname
```      
