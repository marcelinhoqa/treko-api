pipeline {
  agent {
    docker {
      image "node:8-alpine"
    }
  }
  stages {
    stage("Build"){
      steps {
        sh "echo 'http://dl-cdn.alpinelinux.org/alpine/v3.9/main' >> /etc/apk/repositories"
        sh "echo 'http://dl-cdn.alpinelinux.org/alpine/v3.9/community' >> /etc/apk/repositories"
        sh "apk upgrade --update"
        sh "apk update"
        sh "apk add mongodb yaml-cpp=0.6.2-r2"
        sh "chmod +x ./scripts/dropdb.sh"
        sh "mongo -version"
      }
    }
    stage("Test"){
      steps {
        sh "npm run test:ci"
      }
    }
  }
}

