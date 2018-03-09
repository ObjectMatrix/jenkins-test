pipeline {
  agent { label 'docker' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -f "hello-my-alpine" -t node:latest .'
        println "building done."
      }
    }
    stage('Publish') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry([credentialsId: "2d96e761-3947-42c5-8c28-b1248dd17bf7", url: ""]) {
          sh 'docker push asadz31/hello-my-alpine:latest'
          println "done push."
        }
      }
    }
  }
}
