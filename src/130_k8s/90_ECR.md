https://docs.aws.amazon.com/AmazonECR/latest/userguide/docker-push-ecr-image.html

* create image from docker file on M1 Mac
  
  * ```docker buildx build --platform=linux/amd64 -t jksiazek/flask_web_app -f Dockerfile .```
    
    ```

* loging to pgs sandbox
  *```aws ecr get-login-password --region eu-west-1 | docker login --username AWS --password-stdin 890769921003.dkr.ecr.eu-west-1.amazonaws.com```

* tag the image
  
  * ```docker tag <local-image_id> aws_account_id.dkr.ecr.region.amazonaws.com/my-repository:tag```
  * ```docker tag 33195fa51b97 890769921003.dkr.ecr.eu-west-1.amazonaws.com/jksiazek:0.0.2```

* Push the image 
  
  * ``docker push aws_account_id.dkr.ecr.region.amazonaws.com/my-repository:tag``
  * ``docker push 890769921003.dkr.ecr.eu-west-1.amazonaws.com/jksiazek:0.0.1``