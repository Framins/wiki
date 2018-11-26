# Minikube

[Minikube][] = Mini + [Kubernetes][] ，專案的標題也取的非常白話，是本地端執行的 Kubernetes 。

## Setup

[官方的安裝說明](http://kubernetes.io/docs/getting-started-guides/minikube/)，所以它不支援 Windows 安裝

它需要裝三樣東西：

* [Virtualbox](https://www.virtualbox.org/)
* Minikube
* kubectl

Virtualbox 直接上官網裝即可

Minikube 可以上 [release](https://github.com/kubernetes/minikube/releases) 頁面，有指令可以安裝。 kubectl 在官方的說明頁面裡面有安裝指令

[Kubernetes]: https://github.com/kubernetes/kubernetes
[Minikube]: https://github.com/kubernetes/minikube

## Start

啟動非常簡單，只要下

    minikube start

即可

kubectl 在使用之前需先設定 context

    kubectl config use-context minikube

接著下這個指令可以看 kube-system 裡面的 pods

    kubectl get pods --all-namespaces

最後， minikube 也有包含了 [Kubenetes dashboard](http://kubernetes.io/docs/user-guide/ui/) ，下這個指令可以開啟

    minikube dashboard

## References

* [五分鐘 Kubernetes 有感](https://medium.com/@evenchange4/%E4%BA%94%E5%88%86%E9%90%98-kubernetes-%E6%9C%89%E6%84%9F-e51f093cb10b)
