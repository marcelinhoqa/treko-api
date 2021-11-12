pipeline {
  agent {
    docker {
      image "node:8-alpine"
    }
  }
  stages {
    stage("Build"){
      steps {
        sh "apk add --no-cache mongodb" 
        sh "chmod +x ./scripts/dropdb.sh"
        sh "npm install"
      }
    }
    stage("Test"){
      steps {
        sh "npm run test:ci"
      }
    }
  }
}

/*  Por mais que o servidor seja linux, não é possível executar como apt-get install mongodb
por ser uma distribuição do node:alpine é necessário executar como  sh "apk add --no-cache mongodb"    -- no cache pra não pegar cache
*/
