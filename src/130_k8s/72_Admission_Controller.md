* AdmissionControllers
    * examples:
        * only permit images from certain registry
        * do not permit runAs root user
        * pod always has labels


* View admission controllers
  * ```kube-apiserver -h | grep enable-admission-plugins```
  * ```kubectl exec kube-apiserver-controlplane -n kube-system -- kube-apiserver -h | grep enable-admission-plugins```
  * ```ps -ef | grep kube-apiserver | grep admission-plugins```

* AdmissionControllers types:
  * Mutating = runs before Validating Admission Controller
  * Validating

* Creating custom AdmissionController
  * Types
    * MutatingAdmissionWebhook
    * ValidatingAdmissionWebhook
  * Workflow
    * deploy webhook server - code with 2 apis (/validate, /mutate)
    * configure admission controller webhook