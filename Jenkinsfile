pipeline {
    agent any
    
   environment {
       
    registry = "david13356"
    registryCredential = '473db8fb-7b36-4c66-aa81-1e38faa4afdc'
    dockerImage_api = ''
    dockerImage_web = ''
    
   }
  
    stages {
        stage('Clone git') {
             steps {
                 git(credentialsId: '1bd4fb12-1bd4-4f3f-b155-7764792770ab', url: 'https://github.com/DaviAraujoCC/node_simple_app', branch: 'main')
             }
        }
        stage('Build Image') {
            steps {
              dir ('src/web') {
                script {
                     docker.build registry + ":$BUILD_NUMBER"
                     dockerImage_web = docker.build registry + "/node-web-app:v$BUILD_NUMBER"
                }
              }
              dir ('src/api') {
                script {
                     docker.build registry + ":$BUILD_NUMBER"
                     dockerImage_api = docker.build registry +"/node-api-app:v$BUILD_NUMBER"
                }
              }
            }
        }
        stage('Push Image') {
            steps {
              script {
                 docker.withRegistry( '', registryCredential ) {
                 dockerImage_web.push()
                 dockerImage_api.push()
                }
              }
            }
        }
        stage('Remove Unused docker image') {
           steps{
             bat "docker rmi $registry/node-api-app:v$BUILD_NUMBER"
             bat "docker rmi $registry/node-web-app:v$BUILD_NUMBER"
           }
        }
        stage('Deploy Prod') {
            steps {
                container('tools') {
                  sh "git clone https://github.com/DaviAraujoCC/K8s-CICD.git"
                dir("K8s-CICD") {
                  sh "cd ./prod && kustomize edit set image api=david13356/node-api-app:v$BUILD_NUMBER"
                  sh "cd ./prod && kustomize edit set image web=david13356/node-web-app:v$BUILD_NUMBER"
                  sh "git remote add cicd https://github.com/DaviAraujoCC/K8s-CICD.git"
                  sh "git commit -am 'Publish new version $BUILD_NUMBER' && git push cicd main"
                 }
              }
            }
        }
    }
}
