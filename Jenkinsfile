pipeline {
  agent any
  stages {
    stage('Build image') {
      steps {
        sh 'podman build -f ngnix-server:v1 https://raw.githubusercontent.com/Tal-Hason/UpdatePipeline/main/Dockerfile/Dockerfile '
        sh 'sudo yum update -y && sudo yum install podman -y'
      }
    }

  }
}