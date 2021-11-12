pipeline {
  agent {
    docker {
      image "node:8-alpine"
      args "--network=skynet"
    }
  }
  stages {
    stage("Build"){
      steps {
         /*  Por mais que o servidor seja linux, não é possível executar como apt-get install mongodb
         por ser uma distribuição do node:alpine é necessário executar como  sh apk add --no-cache mongodb    -- no cache pra não pegar cache */
        
        sh "echo 'http://dl-cdn.alpinelinux.org/alpine/v3.9/main' >> /etc/apk/repositories"
        sh "echo 'http://dl-cdn.alpinelinux.org/alpine/v3.9/community' >> /etc/apk/repositories"
        sh "apk upgrade --update"
        sh "apk update"
        sh "apk add mongodb yaml-cpp=0.6.2-r2"
        sh "chmod +x ./scripts/dropdb.sh"
        sh "mongo -version"
        sh "npm install"
      }
    }
    stage("Test"){
      steps {
        sh "npm run test:ci"
      }
      post {    //mesmo que falhe o teste ou não o método post envia 
        always { // always vai enviar SEMPRE
          junit "log/*.xml"  // plugin junit já vem por padrão no jenkins, esse comando ele lé a pasta log e publica o resultado no jenkins
        }
      }
    }
    stage("Production"){
      steps {
          input message: "Go to production? (Clik 'Proced' to continue)"
          sh "echo 'subindo em produção'"
      }
    }
  }
}

