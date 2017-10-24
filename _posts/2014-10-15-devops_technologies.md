---
layout: post
title:  "Devops technologies"
tags:
- devops
permalink: /2014/10/15/devops-technologies
published: false
---


### Source Control

  * subversion
  * git (stash/Github/gitlab)

### Integration Environment

  * API based infrastructure provider, e.g. vSphere/AWS/Rackspace Cloud
  * Vagrant

### Documentation

  * Markdown
  * Wiki markup / Confluence

### Build System

  The collection of tooling that enables continuous integration of commits
  by building the software, running any tests and deploying to integration
  environments.

  Status of all steps needs to be broadcast to all interested parties, and
  testing should include not just normal TDD/unit tests but also should look
  into the following:-

  * security
  * infrastructure regression
  * code lint
  * performance

  General technologies below

  * Jenkins
  * Puppet/Hiera (enabling)
  * serverspec (enabling)
  * Docker (emerging/enabling)


### Monitoring/Metrics/Logging

  * New Relic
  * Sensu
  * Graphite
  * Logstash/ElasticSearch
  * Kibana/Grafana
  * SAAS - logentries, boundary networks (emerging)

### Communications

  * skype
  * slack (emerging)
  * hubot [https://hubot.github.com]

### Code Review

  This group should enable team members to improve code quality, and ensure that

  * integrated with git provider typically
  * pull requests / peer review for merge into branch/master

### Issue Tracking

  * Atlassian Jira

### Operating Systems/Distributions

  * Centos/RHEL
  * CoreOS (emerging)

### Databases/Datastore

  * MySQL
  * MongoDB
  * Redis -
