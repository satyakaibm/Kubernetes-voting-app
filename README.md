# Kubernetes-voting-app
For successful Deployment of the whole app, we need to run the kubectl in sequencial order
1. create the pod for voting-app-pod 
$ kubectl create -f voting-app-pod.yaml
pod/voting-app-pod created

2. create and voting-service 
$ kubectl create -f voting-app-service.yaml
service/voting-service created

3. confirm the pod and service created properly or not
$ kubectl get pods,svc
NAME                 READY   STATUS    RESTARTS   AGE
pod/voting-app-pod   1/1     Running   0          101s

NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
service/kubernetes       ClusterIP   10.96.0.1       <none>        443/TCP        150d
service/voting-service   NodePort    10.103.240.96   <none>        80:30004/TCP   56s

4. Check the service in browser
$ minikube service voting-service --url
http://192.168.99.101:30004

5. $ kubectl create -f redis-app-pod.yaml
pod/redis-pod created

6. create the redis service 
$ kubectl create -f redis-service.yaml
service/redis created

7. create the postgres pod 
$ kubectl create -f postgres-pod.yaml
pod/postgres-pod created

8. create the postgres service 
$ kubectl create -f postgres-service.yaml
service/db created

9. check the pod and services creating properly or not.
$ kubectl get pods,svc
NAME                 READY   STATUS    RESTARTS   AGE
pod/voting-app-pod   1/1     Running   0          10m
pod/redis-pod        1/1     Running   0          4m17s
pod/postgres-pod     1/1     Running   0          2m19s

NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
service/voting-service   NodePort    10.103.240.96   <none>        80:30004/TCP   10m
service/redis            ClusterIP   10.98.45.126    <none>        6379/TCP       3m57s
service/db               ClusterIP   10.111.23.57    <none>        5432/TCP       2m12s

10. create the worker pod 
$ kubectl create -f worker-app-pod.yaml
pod/worker-app-pod created

11. create the result app pod 
$ kubectl create -f result-app-pod.yaml
pod/result-app-pod created

12. create the result service 
$ kubectl create -f result-app-service.yaml
service/result-service created

13. Lets check all the pods and services
$ kubectl get pods,svc
NAME                 READY   STATUS             RESTARTS   AGE
pod/postgres-pod     1/1     Running            0          12m
pod/redis-pod        1/1     Running            0          14m
pod/result-app-pod   1/1     Running            0          7m9s
pod/voting-app-pod   1/1     Running            0          20m
pod/worker-app-pod   0/1     ImagePullBackOff   0          8m12s

NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
service/db               ClusterIP   10.111.23.57    <none>        5432/TCP       12m
service/kubernetes       ClusterIP   10.96.0.1       <none>        443/TCP        150d
service/redis            ClusterIP   10.98.45.126    <none>        6379/TCP       13m
service/result-service   NodePort    10.105.5.216    <none>        80:30005/TCP   6m20s
service/voting-service   NodePort    10.103.240.96   <none>        80:30004/TCP   20m

14. Check the services in browser
$ minikube service voting-service --url
http://192.168.99.101:30004

$ minikube service result-service --url
http://192.168.99.101:30005
