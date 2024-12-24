# K8s 명령어

k8s 사이트에서 다운로드 할 것
- minikube: 로컬환경에서 가상머신을 이용해 인프라를 구축시켜줌 => PoC용
- kubectl: cluster 안에 설계할 수 있는 명령어

1. k8s 환경설정

```
minikube start --driver=docker
minikube status
minikube dashboard
```

2. 이미지 만들기 => dockerhub에 public으로 올려야함! 로컬머신에 이미지를 만든다고 k8s가 접근하는 것이 아님

```
docker tag <이미지이름> <docker사용자명>/<이미지이름>
docker push <docker사용자명>/<이미지이름>
```

3. kubectl로 deployment 만들기 및 확인

```
kubectl create deployment <deployment이름> --image=<docker사용자명>/<이미지이름>
kubectl get deployments
kubectl get pods
```
   
