* Rollout status
  * ```kubectl rollout status deployment/<deployment-name>``` - print deployment status  
  * ```kubectl rollout history deployment/<deployment-name>``` - print history  

* Rolling update
  * ```kubectl edit deployment <name-of-deployment>``` - edit and change image - triggering rolling deployment
  * ```kubectl set image deployment <name-of-deployment> nginx=nginx:1.9.1``` - setting new image
  * ```kubectl rollout status deployment/<name-of-deployment>``` - rollout status
  * ```kubectl rollout undo deployment/<name-of-deployment>``` - getting back to the latest version

* Rollback
  * ```k rollout undo deployment/<deployment-name>``` - rollback undo to last running deployment

* Blue/green update
  * istio - good implemention 
  * create 1 service and 2 deployments green and blue
  * switching to new version with changing the label in service from i.e. v1 -> v2
  * deploy(blue) v=1, service ```v1```, deploy(green) v=2 -> deploy(blue) v=1, service ```v2```, deploy(green) v=2

* Canary 
  * adding new version alongside old version 
  * route small percentage to new version
  * ie. 3 pods - old version, 1 pod - new version 
  * deploy(old) l=version=v1,app=front-end, service ```l=app=front-end```, deploy(green) l=version=v2,app=front-end