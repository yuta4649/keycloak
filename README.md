# keycloak
## Ingressでの外部公開手順
### Deploy Keycloak
```bash
kubectl apply -f ingress/deployments.yml
```
### Deploy Ingress
```bash
# minikube addons list を実行し、ingressがenableになっていることを確認する。enable出ない場合は以下を実行
minikube addons enable ingress
kubectl apply -f ingress/ingress.yml
```

## NodePortでの外部公開手順
### Deploy Keycloak
```bash
kubectl apply -f nodeport/deployments.yml
# 外部に公開するServiceを作成する
kubectl expose deployment keycloak --port=8080 --type=NodePort
# 以下コマンドを実行するとブラウザに表示される
minikube service keycloak
```
