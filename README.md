LOCAL NOTEs:

VISO - CONFIG SERVER
MAVEN:
PS D:\...\ configserver> mvn clean install

-> start Docker Desktop
-> delete old images from LOCAL & docker hub REPO
-> start following containers on Docker Desktop
     - zipkin
     - prometheus
     - grafana

DOCKER:
PS D:\...\ configserver> docker build -t longlethanh/viso-configserver:0.0.1-SNAPSHOT .
PS D:\...\ configserver> docker push longlethanh/viso-configserver:0.0.1-SNAPSHOT

K8S:
PS D:\...\configserver> cd k8s
PS D:\...\configserver\k8s> minikube start

PS D:\...\configserver\k8s> kubectl get services
PS D:\...\configserver\k8s> kubectl delete services srv1 srv2

PS D:\...\configserver\k8s> kubectl get deployments
PS D:\...\configserver\k8s> kubectl delete deployments dep1 dep2
-> replica sets are implicitly removed then the child-pods will be automatically deleted

PS D:\...\configserver\k8s> dir
PS D:\...\configserver\k8s> kubectl create -f cs-deploy-repset-pods.yml
PS D:\...\configserver\k8s> kubectl create -f configserver-service.yml
PS D:\...\configserver\k8s> minikube dashboard

PS D:\...\configserver\k8s> kubectl port-forward service/viso-configserver-service 7088:8888

TEST:
http://localhost:7088/walletservice/default

<service-name>.<namespace>.svc.cluster.local:<service-port>
viso-configserver-service.default.svc.cluster.local:8888
