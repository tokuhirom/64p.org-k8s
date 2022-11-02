# 64p.org-k8s

自分のホームページを k8s 上に構築する。

## DigitalOcean's k8s の初期設定

以下のように設定する。

    brew install helm
    brew install doctl
    doctl auth init --context blog3
    doctl auth list
    doctl auth switch --context blog3
    doctl kubernetes cluster kubeconfig save <<CLUSTER_ID>>

## Secret operation

    kubectl create secret generic mysql-user-pass --from-literal=url=${URL} --from-literal=username=${USERNAME} --from-literal=password=${PASSWORD}
    kubectl create secret generic security-user-pass --from-literal=username=${USERNAME} --from-literal=password=${PASSWORD}

消すときは以下の様にする。

    kubectl delete secret mysql-user-pass

## Apply Operation

    kubectl apply -f k8s/app-server.yml
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.4.0/deploy/static/provider/do/deploy.yaml
    kubectl apply -f k8s/ingress-nginx.yml

Apply all files:

    kubectl apply -f

## architecture

 * ingress nginx

## Words

 * pod
 * node
  * vm/pm instance
  * a worker machine in k8s, part of a cluster
 * ingress
  * An API object that manages external access to the services in a cluster, typically HTTP.

## Show ingress info


    $ kubectl get ing
    NAME                CLASS    HOSTS                  ADDRESS          PORTS   AGE
    blog3-app-ingress   <none>   blog-staging.64p.org   157.230.192.20   80      4d12h

    $ kubectl describe ing blog3-app-ingress
    Name:             blog3-app-ingress
    Labels:           <none>
    Namespace:        default
    Address:          157.230.192.20
    Ingress Class:    <none>
    Default backend:  <default>
    Rules:
    Host                  Path  Backends
    ----                  ----  --------
    blog-staging.64p.org
                            /   blog3-app-server:8080 ()
    Annotations:            kubernetes.io/ingress.class: nginx
    Events:                 <none>




## Next step

 * split blog3's admin site
 * include 64p.org top page
 * cert support

## see also

ref. https://www.javachinna.com/deploy-angular-spring-boot-mysql-digitalocean-kubernetes/
https://www.youtube.com/watch?v=r0NpHb-6IvY


