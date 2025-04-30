pipeline {
    agent any

    stages {
        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout SCM') {
            steps {
                git branch: 'main', credentialsId: 'id-jenkins-github', url: 'https://github.com/JasonGagnard/projet-dev01.git'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    sh 'docker build -t myimage_nginx .'
                    sh 'docker tag myimage_nginx myimage_nginx:youyou'
                }
            }
        }

        stage('Deploy App') {
            steps {
                script {
                  

                    // Arrêter le conteneur s'il est en cours d'exécution
                    sh 'docker stop monapp '

                    // Supprimer le conteneur s'il existe
                    sh 'docker rm monapp '

                    // Lancer le nouveau conteneur
                    sh 'docker run -d --name monapp --hostname monapp -p 8089:80 myimage_nginx:youyou'
                      // Supprimer l'ancienne image si elle existe
                    sh 'docker image rm -f myimage_nginx || true'
                    sh 'docker exec monapp ifconfig'
                }
            }
        }
    }
}
