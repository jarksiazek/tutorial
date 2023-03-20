###Deployment
* Create a deployment with image nginx:1.18.0, called nginx, having 2 replicas, defining port 80 as the port that this container exposes (don't create a service for this deployment)
  * ```kubectl create deploy nginx --image=nginx:1.18.0 --replicas=2 --port=80```
* View the YAML of this deployment
  * ```kubectl get po nginx -o yaml```
* View the YAML of the replica set that was created by this deployment
  * ```kubectl get rs -l app=nginx # if you created deployment by 'create' command```
* Get the YAML for one of the pods
  * ```kubectl get pod -l app=nginx # if you created deployment by 'create' command```
* Check how the deployment rollout is going
  * ```kubectl describe deploy nginx | grep deployment```
  * ```kubectl rollout status deploy nginx```
* Update the nginx image to nginx:1.19.8
  * ```kubectl set image deploy nginx nginx=1.19.8```
* Check the rollout history and confirm that the replicas are OK
  * ```kubectl rollout history deploy nginx ```
* Undo the latest rollout and verify that new pods have the old image (nginx:1.18.0)
  * ```kubectl rollout undo deploy nginx```
* Return the deployment to the second revision (number 2) and verify the image is nginx:1.19.8 
  * ```kubectl rollout history deploy nginx```
  * ```kubectl rollout undo deploy nginx --to-revision=2```
* Check the details of the fourth revision (number 4) 
  * ```kubectl rollout history deploy nginx --revision=4```
* Scale the deployment to 5 replicas
  * ```kubectl scale deploy nginx --replicas=5```
* Autoscale the deployment, pods between 5 and 10, targetting CPU utilization at 80%
  * ```kubectl autoscale deploy nginx --min=5 --max=10 --cpu-percent=80```
  * # view the horizontalpodautoscalers.autoscaling for nginx
  * ```kubectl get hpa nginx```
* Autoscale the deployment, pods between 5 and 10, targetting CPU utilization at 80% 
  * ```kubectl autoscale deploy nginx --min=5 --max=10 --cpu-percent=80```
* Pause the rollout of the deployment
  * ```kubectl rollout pause deploy nginx```

### Do it!!
* Implement canary deployment by running two instances of nginx marked as version=v1 and version=v2 so that the load is balanced at 75%-25% ratio
  * 