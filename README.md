# k8s-project
Final project - DevOps expert 

Docker create images base on https://github.com/avielb/rmqp-example

docker build ./producer/ -t gals/producer

docker build ./consumer/ -t gals/consumer

docker tag gals/producer gals/producer:1.0.0

docker tag gals/consumer gals/consumer:1.0.0


docker push  gals/producer:1.0.0
docker push gals/consumer:1.0.0

docker push gals/producer:latest
docker push gals/consumer:latest



Rabbitmq configure 

helm search repo | grep rabbitmq

Install:

helm install my-rabbitmq bitnami/rabbitmq --set service.type=NodePort


get conntcions 
echo "Username      : user"                                                                                                                 
echo "Password      : $(kubectl get secret --namespace default my-rabbitmq -o jsonpath="{.data.rabbitmq-password}" | base64 --decode)"      
echo "ErLang Cookie : $(kubectl get secret --namespace default my-rabbitmq -o jsonpath="{.data.rabbitmq-erlang-cookie}" | base64 --decode)" 


 export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")           
 export NODE_PORT_AMQP=$(kubectl get --namespace default -o jsonpath="{.spec.ports[1].nodePort}" services my-rabbitmq)   
 export NODE_PORT_STATS=$(kubectl get --namespace default -o jsonpath="{.spec.ports[3].nodePort}" services my-rabbitmq)  


install export 

helm install my-prometheus-rabbitmq-exporter prometheus-community/prometheus-rabbitmq-exporter --set service.type=NodePort