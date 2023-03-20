###CronJob
* Create a cron job with image busybox that runs on a schedule of "*/1 * * * *" and writes 'date; echo Hello from the Kubernetes cluster' to standard output
  * ```kubectl create cronjob busybox --image=busybox --schedule="*/1 * * * * -- /bin/sh -c 'date; echo Hello from the Kubernetes cluster'```"
* See its logs and delete it
  * ```kubectl logs busybox-***```
* Create a cron job with image busybox that runs every minute and writes 'date; echo Hello from the Kubernetes cluster' to standard output. The cron job should be terminated if it takes more than 17 seconds to start execution after its scheduled time (i.e. the job missed its scheduled time).
  * ```kubectl create cronjob busybox --image=busybox --schedule="*/1 * * * * -- /bin/sh -c 'date; echo Hello from the Kubernetes cluster' ```
  * ```add  spec.startingDeadlineSeconds = 17```
* Create a cron job with image busybox that runs every minute and writes 'date; echo Hello from the Kubernetes cluster' to standard output. The cron job should be terminated if it successfully starts but takes more than 12 seconds to complete execution.
  * ```kubectl create cronjob busybox --image=busybox --schedule="*/1 * * * * -- /bin/sh -c 'date; echo Hello from the Kubernetes cluster' ```
  * ```Add cronjob.spec.jobTemplate.spec.activeDeadlineSeconds=12```