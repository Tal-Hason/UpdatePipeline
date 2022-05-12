pipeline {
  agent any
    stages {
        stage("Create ConfigMap") {
            steps {
                sh 'oc create configmap html-index --from-file=application/index.html --dry-run=client -o yaml | oc apply -f -'
           }
        }   
        stage("Run Application from Docker file") {
            steps {
                sh 'oc new-app --name=ngnix-hello-world . --strategy=docker --context-dir=Dockerfile' 
            }
        }
        stage("Map ConfigMap as a Volume") {
            steps {
                sh 'oc set volume deployments/nginx-hello-world --add --name=index-html --type=configmap --configmap-name="html-index" --mount-path=/usr/share/nginx/html'
            }
        }
    }
}