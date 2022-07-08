* Container Logging
   * ```kubectl logs -f <pod-name>``` - option for one contrainer in the pod
   * ```kubectl logs -f <pod-name> <container-name>``` - option for multi contrainers in the pod  
   * ```kubectl logs -l app=<label_app_name> -f``` - getting logs from all pods for specific app
     