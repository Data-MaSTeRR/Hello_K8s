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

## 명령적 접근방식 kubectl

1. deployment 만들기 및 확인 => pod도 같이 생성

```
kubectl create deployment <deployment이름> --image=<docker사용자명>/<이미지이름>,<docker사용자명>/<이미지이름> ...
kubectl get deployments
kubectl get pods
```

2. service를 만들어 외부로 노출

```
kubectl expose deployment <deployment이름> --type=LoadBalancer --port=8080
kubectl get services
```

3. 외부IP 열기

```
minikube service <service이름>
```

4. Scaling

```
kubectl scale deployment/<deployment이름> --replicas=3
```

5. Deployment 이미지 교체 => 이미지가 dockerhub에 있어야 함

```
docker push datamasterr/<이미지이름>:2 # tag 달아서 구분해줘야 함
docker set image deployment/<deployment 이름> <이전이미지이름>=<datamasterr/새로운이미지이름:2>
```

6. Deployment rollout => undo, status, history

```
kubectl rollout undo deployment/<deployment 이름> # 전단계로 deployment 돌아감
kubectl rollout undo deployment/<deployment 이름> # 전단계로 deployment 돌아감
```

## 선언적 접근방식


