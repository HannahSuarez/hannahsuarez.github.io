---
layout: post
title: "Cloud Native Security Workshop notes"
description: "Workshop notes from a recent cloud native security workshop delivered by Component Soft"
comments: true
keywords: "kubernetes, docker, cloud, cloud security, devops"
---

> This is not a sponsored post. In fact, none of the posts in my blog is sponsored but I just thought to mention it here.

Most recently I did an all day cloud native security workshop. No screenshots or in-depth/detailed notes here but I will share some very useful notes, tips and resources. Kubernetes and Docker were the main platforms provided.

The workshop was very thorough and covered secure deployment, penetration testing, security monitoring, proper access rights, etc. It was a small group - about 10 people at the start and went down to 6 people due to having to leave, etc.

Much of it was theory, but it was quiet important to understand how things work. For example, knowing how the Kubernetes API work was important, the concept of a Helper application, etc.

---

## Recommended tools from the workshop

* [DEX](https://github.com/dexidp/dex/blob/master/Documentation/kubernetes.md)
* [Harbor](https://goharbor.io/)
* [Falco](https://github.com/falcosecurity)
* [Kube-hunter](https://github.com/aquasecurity/kube-hunter)
* [Kube-bench](https://github.com/aquasecurity/kube-bench)
* [Sonobuoy](https://github.com/vmware-tanzu/sonobuoy)
* [securityhub](https://securityhub.dev)
