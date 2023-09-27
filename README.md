# keycloak
## Ingressでの外部公開手順
こちらの手順はDockerでminikubeを起動しいている場合はingressコントローラーが起動しないため実施できない。調査は続け、問題解消し次第試す。
### Deploy Keycloak
```bash
kubectl apply -f ingress/deployments.yml
```
### Deploy Ingress
```bash
# minikube addons list を実行し、ingressがenableになっていることを確認する。enable出ない場合は以下を実行
minikube addons enable ingress
kubectl apply -f ingress/ingress.yml
# 以下コマンドを実行しホストマシンとMinikubeクラスタ内のサービス間のネットワークルーティングを設定
minikube tunnel
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
