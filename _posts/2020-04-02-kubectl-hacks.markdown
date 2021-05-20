---
title: "Kubectl Hacks - Be productive"
layout: post
date: 2020-04-02 15:00
tag:
- kubernetes
- k8s
- kubectl
- cloud
- sre
- devops
- infrastructure


headerImage: true
image: /assets/k8s.png
hidden: false # don't count this post in blog pagination
description: "Useful kubectl plugins and extensions"
jemoji: ""
category: blog
author: adityachowdhry
externalLink: false
---

At [Gojek](https://www.gojek.io/), I have been playing around with [kubernetes](https://kubernetes.io/) for a few months now. Spending more and more time with its command line interface — ***[kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)***

This post talks about extending kubectl with few of the plugins that have been useful to me in day to day debugging/maintaining things on k8s.

![Photo by Carl Heyerdahl on Unsplash](https://images.unsplash.com/photo-1587571164348-b04475b8bd2d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2100&q=80)


Note: I am using zsh, so some of them are ohmyzsh plugins

Lets go through them!

## [ohmyzsh kubectl](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/kubectl)

This plugins provides aliases for common *kubectl* commands. You can get complete list of aliases here — [kubectl-aliases](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/kubectl#aliases)

Few examples

- k for `kubectl` — The kubectl command
- kgp for `kubectl get pods` — List all pods in ps output format
- kgswide for `kgs -o wide` — After listing all services, output in plain-text format with any additional information

![Image](/assets/images/kubectl-aliases.png) *Kubectl aliases*

## [kubectx + kubens](https://github.com/ahmetb/kubectx/) — Power tools for kubectl (+ [fzf](https://github.com/junegunn/fzf) )

If you work with multiple clusters or namespaces then this tool is a blessing.

- **kubectx** — helps you switch between clusters back and forth
- **kubens** — helps you switch between namespaces back and forth

Kubectx             |  Kubens
:-------------------------:|:-------------------------:
![kubectx](/assets/images/kubectx.gif)  |  ![kubens](/assets/images/kubens.gif)

It shortens

- Setting context: `kubectl config get-contexts` and `kubectl config use-context <context-name>`
- Setting namespace: `kubectl get namespaces` and `kubectl config set-context --current --namespace=<namespace>`

Along with [fzf](https://github.com/junegunn/fzf) — A command-line fuzzy finder, it gives an interactive menu to select the context/namespace as shown above in gif

## [kube-ps1](https://github.com/jonmosco/kube-ps1) or [zsh-kubectl-prompt](https://github.com/superbrothers/zsh-kubectl-prompt)

When dealing with multiple contexts and namespaces, it becomes confusing to determine what is the current context/namespace you are working on.

You can check for the current context/namespace using `kubectl config current-context` and `kubectl config view` to determine current namespace. This is fine when you are not dealing with multiple contexts and don’t have to switch frequently.

But if you do, this can be a saviour when doing certain operations or debugging production incidents where you have to change contexts frequently. Any wrong step and you can end up doing destructive operations on wrong cluster.

kube-ps1 or zsh-kubectl-prompt adds context and namespace upfront in your prompt, so that you can be sure of cluster and namespace you are working on.

![zsh-kubectl-prompt](/assets/images/context-1.png)
*zsh-kubectl-prompt*

![kube-ps1](/assets/images/context-2.png)
*kube-ps1*

## [kubetail](https://github.com/johanhaleby/kubetail)
A tiny bash script to tail multiple pod logs in single stream. It is simply `kubectl logs -f` but for multiple pods.

You can do regex matching on pods, view specific container logs or can simply give multiple pods. This tool comes in handy when debugging issues with our applications.
![kubetail](/assets/images/kubetail.png)
*kubetail in action*

## [kubespy](https://github.com/pulumi/kubespy)
Kubespy tools help in observing Kubernetes resources in real time. This is useful when you want to keep a track of resources on various actions you perform.

checkout kubespy in action —
![kubespy](/assets/images/kubespy.gif)
*kubespy observing deployment resource status changes*

* * *

These were a small set of plugins that I use in day to day activities. K8s have its own plugin package manager named as [krew](https://github.com/kubernetes-sigs/krew). They have around 70 plugins — do check them out [here](https://github.com/kubernetes-sigs/krew-index/blob/master/plugins.md)


## [K9s - Kubernetes CLI To Manage Your Clusters In Style!](https://github.com/derailed/k9s)
K9s provides a terminal UI to interact with your Kubernetes clusters. The aim of this project is to make it easier to navigate, observe and manage your applications in the wild. K9s continually watches Kubernetes for changes and offers subsequent commands to interact with your observed resources.

***Let me know if these were useful to you as well. If you have any suggestions do comment!***