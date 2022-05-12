pipeline {
  agent any
    stages {
        stage("Create New Project") {
            steps {
                sh 'oc new-project ngnix-hello-world'
           }
        }
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
        stage("Test service is Running") {
            steps{
                timeout(5) {
                    waitUntil {
                        script {
                            def r = sh script: 'wget -q http://ngnix-hello-world.application-version.svc.cluster.local:8080/index.html -O /dev/null', returnStdout: true
                            return (r == 0);
                        }
                    }
                }
            }
        }
        stage("Map ConfigMap as a Volume") {
            steps {
                sh 'oc set volume deployments/ngnix-hello-world --add --name=index-html --type=configmap --configmap-name="html-index" --mount-path=/usr/share/nginx/html'
            }
        }
    }
}