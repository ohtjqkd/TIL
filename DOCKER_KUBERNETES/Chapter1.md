# Docker Base

## What is Docker?
![docker vs virtual machine](https://k21academy.com/wp-content/uploads/2020/05/2020_05_13_12_19_07_PowerPoint_Slide_Show_Azure_AZ104_M01_Compute_ed1_-1024x467.png)

- 가상머신은 하나의 물리서버를 효율적으로 사용하면서 격리 환경을 제공해주기 위해서 사용한다. 하지만 이런 가상머신은 하드웨어 자원들을 에뮬레이션하여 사용하기 때문에 성능효율성이 많이 떨어지고, 오버헤드가 증가하게 된다. 이를 해결하고자 만들어진 기술 개념이 컨테이너임, chroot, namespace 등의 기술을 사용하여 격리 환경을 제공함

## How to Install

설치가이드 페이지(https://docs.docker.com/engine/install/ubuntu/)


```

# uninstall oldversion
sudo apt-get remove docker docker-engine docker.io containerd runc

# Set up the repository

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt-update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Group add
sudo usermod docker $USER or target_user
```
필요하다면 script로 만들어 편리하게 사용할 수 있음

## kubectl and kustomize Install
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
```
## INFO: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management

set -euf -o pipefail

# Install dependencies
sudo apt-get update && sudo apt-get install -y \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg \
  lsb-release

# Add kubectl's official GPG key
curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /usr/share/keyrings/kubernetes-archive-keyring.gpg

# Set up the repository
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

# Install kubectl
sudo apt-get update && sudo apt-get install -y kubectl
```

## minikube install

```
#!/usr/bin/env bash
## INFO: https://minikube.sigs.k8s.io/docs/start/

set -euf -o pipefail

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
