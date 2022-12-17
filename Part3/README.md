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

**#kubectl set image deployment/webapp nginx=nginx:1.17.4  --record**
**#kubectl describe deploy webapp**

8. Check the rollout history and make sure everything is ok after the update

**#kubectl rollout history deploy webapp**
**#kubectl get deployment**

9. Undo the deployment to the previous version 1.17.1 and verify Image has the previous version

**#kubectl rollout undo deploy webapp**
**#kubectl describe deploy webapp**

10. Update the deployment with the wrong image version 1.100 and verify something is wrong with the deployment

**#kubectl set image deploy webapp nginx=nginx:1.100**
**#kubectl rollout status deploy webapp**
**#kubectl rollout undo deploy webapp**
**#kubectl rollout history deploy webapp --revision=7  -  throws an error**
**#kubectl rollout history deploy webapp**
**#kubectl set image deployment/webapp nginx=nginx:latest --record**
**#kubectl rollout history deploy webapp**

11. Apply the autoscaling to this deployment with minimum 10 and maximum 20 replicas and target CPU of 85% and verify hpa is created and replicas are increased to 10from 1

**#kubectl autoscale deployment webapp --cpu-percent=85 --min=10 --max=20**
**#kubectl get hpa**
**#kubectl get pods**

13. Clean the cluster by deleting deployment and hpa you just created

**#kubectl delete deploy webapp**
**#kubectl delete hpa**

14. Create a job and make it run 10 times one after one (run > exit > run >exit ..) using the following configuration:
**#kubectl create job hello-job --image=busybox --dry-run -o yaml -- echo "Hello I am from job" > hello-job.yaml”**
