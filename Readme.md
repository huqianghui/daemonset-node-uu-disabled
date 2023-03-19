# AKS Node Installer

Many customers want the ability to run arbitrary software on their AKS worker nodes such as Malware scanners, policy enforcers etc. This script which is heavily inspired by [Kured](https://github.com/weaveworks/kured) lets you do that. The script (in the container) is meant to run as a DaemonSet so that new nodes can be bootstrapped.

## Installation

Before installing update the script in k8s/sampleconfigmap.yaml which is run to install the software that you want in the cluster.

```sh
git clone https://github.com/patnaikshekhar/AKSNodeInstaller
cd AKSNodeInstaller
# Update script in ./k8s/sampleconfigmap.yaml to use your installation instructions
kubectl apply -f ./k8s
```

## Explanation
This [blog article](https://medium.com/@patnaikshekhar/initialize-your-aks-nodes-with-daemonsets-679fa81fd20e) explains the code.

## Demo
[![Youtube Demo](https://img.youtube.com/vi/vAIW4ZSP44I/0.jpg)](https://www.youtube.com/watch?v=vAIW4ZSP44I)


需要注意的几点内容：

1） 如果需要访问node节点上的东西，需要配置hostPID: true 和 privileged: true

2） 在上面基础上通过nsenter命令进入node (https://www.cnblogs.com/liugp/p/16344594.html)

3） 在原来的sample之上，如果是ubuntu 18+ 的话，如果需要访问网络的话，需要增加 -n 参数 

4） 通过node-shell 登录到节点之后，ubutun的path是user/games,需要执行PATH=$PATH:/usr/games 才能使用新安装的命令： cowsay moo
    bug link: https://github.com/Microsoft/WSL/issues/203
    
