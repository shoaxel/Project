PART1 

1. Deploy a pod named nginx-pod using the nginx:alpine image. Name: nginx-pod-yourname Image: nginx:alpine
#kubectl run nginx-pod-shosh --image=nginx:alpine

2. Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg.
#kubectl run messaging --image=redis:alpine --labels tier=msg

3. Create a namespace named apx-x998-yourname.
#kubectl create ns apx-x998-shosh

4. Get the list of nodes in JSON format and store it in a file at /tmp/nodes-yourname
#kubectl get nodes -o json > /tmp/shosh

5. Create a service messaging-service to expose the messaging application within the cluster on port 6379.
Use imperative commands - kubectl, Service: messaging-service, Port: 6379, Type: ClusterIp, Use the right labels
#kubectl expose pod messaging --name=messaging-service --port 6379 OR kubectl expose pod messaging --type=ClusterIP --port 6379 --target-port 6379 --name messaging-service --labels tier=msg
