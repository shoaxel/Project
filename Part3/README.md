1. Create a deployment called webapp with image nginx with 5 replicas. Use the below command to create a yaml file

**#kubectl create deploy webapp --image=nginx --dry-run -o yaml > webapp.yaml**
**#Added 5 replicas to webapp.yaml**

2. Get the deployment rollout status

**#kubectl rollout status deploy webapp**

3. Get the replicaset that created with this deployment

**#kubectl get replicaset**

4. EXPORT the yaml of the replicaset and pods of this deployment

**#kubectl get replicaset -o yaml > webapp_rs.yaml**
**#kubectl get pods -o yaml > webapp_po.yaml**

5. Delete the deployment you just created and watch all the pods are also being deleted

**#kubectl delete deploy webapp**

6. Create a deployment of webapp with image nginx:1.17.1 with container port 80 and verify the image version
a. kubectl create deploy webapp --image=nginx:1.17.1 --dry-run -o yaml > webapp_nginx.yaml

7. Update the deployment with the image version 1.17.4 and verify

#kubectl set image deploy webapp nginx=nginx:1.17.4
