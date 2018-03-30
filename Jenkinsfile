pipeline {
  agent { label 'docker' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  triggers {
    cron('@daily')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -f "Dockerfile" -t asadz31/alpine:latest .'.'
        print 'build completed stage'
      }
    }

    stage('Publish') {
        when {
          branch 'master'
        }
        steps {
          withDockerRegistry([credentialsId: "2d96e761-3947-42c5-8c28-b1248dd17bf7", url: ""]) {
            sh 'docker push asadz31/alpine:latest'
            # sh 'docker push asadz31/cli:latest'
            print 'push to docker registry'
          }
        }
      }
    }
}
