Structure
* Chart.yaml -> chart name, dependencies, version, etc
* LICENSE 
* markdown-formatted chard description
* values.yaml - predefined values
* values.schema.json - provides an optional schema for values.yaml
* charts/ - folder, where dependencies are downloaded
* crds/ - custom resource definition (CRDs)
* templates/ - are passed through the template engine, combined with values.yaml
* templates/NOTES.txt - text file is printed out post-installation

Example:
```yaml
image:
  registy: docker.io
  repository: {{ .Values.image.registy }}
  
```



Chart template language
