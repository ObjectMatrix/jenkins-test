pipeline {
  agent { label 'docker' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '2'))
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -f "hello-my-alpine" -t alpine:latest .'
        # sh 'docker build -f "Dockerfile-cli" -t brightbox/cli:latest .'
      }
    }
    stage('Publish') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry([ credentialsId: "2d96e761-3947-42c5-8c28-b1248dd17bf7", url: "https://hub.docker.com" ]) {
          sh 'docker push asadz31/hello-my-alpine:latest'
          #sh 'docker push brightbox/cli:latest'
        }
      }
    }
  }
}
