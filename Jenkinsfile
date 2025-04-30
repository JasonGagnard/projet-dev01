pipeline{
  agent any
  environment{
    IMG_NAME = 'med-nginx'
    DOCKER_REPO = 'test'
  }
  
  stages{
    stage('clean up'){
      steps{
        deleteDir()
      }
    }

    stage('Checkout SCM'){
      steps{
        git (
          branch: 'master',
          url: 'https://github.com/JasonGagnard/projet-dev01.git'
        )
      }
    }
    stage('Build'){
      steps{
        script {
          sh "docker build -t ${IMG_NAME} ."
          sh "docker tag ${IMG_NAME} ${DOCKER_REPO}:${IMG_NAME}"
        }
      }
    }

    stage('deploiement conteneur'){
      steps{
        script {
          sh "docker image prune"
          sh "docker stop monapp || true"
          sh "docker rm monapp || true"
          sh "docker run -d --name monapp --hostname monapp -p 8585:80 ${IMG_NAME}"
          sh 'docker exec monapp "ifconfig"'
        }
      }
    }

  }
}

