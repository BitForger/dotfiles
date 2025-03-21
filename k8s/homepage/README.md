# Homepage Config

## Overview
This directory contains the configuration files for the [homepage project](https://gethomepage.dev).

## Requirements

- [Kustomize](https://kubernetes-sigs.github.io/kustomize/) v4.5.7 or later
- [Kubectl](https://kubernetes.io/docs/tasks/tools/) v1.28.0 or later
- [1Password CLI](https://developer.1password.com/docs/cli/) v2.15.0 or later

## Installation
```sh
kustomize build . | op inject | kubectl apply -f -
```