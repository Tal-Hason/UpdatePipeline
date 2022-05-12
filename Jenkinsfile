pipeline {
  agent any
  stages {
    stage('Build image') {
      steps {
        sh 'yum update -y && yum install podman -y'
        sh 'podman build -f ngnix-server:v1 https://raw.githubusercontent.com/Tal-Hason/UpdatePipeline/main/Dockerfile/Dockerfile '
      }
    }

  }
}