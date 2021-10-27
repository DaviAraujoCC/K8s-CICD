pipeline {
    agent any
    tools {node "node12"}

   environment {
       
    registry = "david13356"
    registryCredential = '473db8fb-7b36-4c66-aa81-1e38faa4afdc'
    dockerImage_api = ''
    dockerImage_web = ''
    
   }
  
    stages {
        stage('Checkout app/binaries') {
             steps {
                 git(credentialsId: '1bd4fb12-1bd4-4f3f-b155-7764792770ab', url: 'https://github.com/DaviAraujoCC/node_simple_app', branch: 'main')
             }
        }
        stage('Build node app') {
            steps {
              dir ('src/web') {
                bat 'npm install'
              }
            }
            /*  dir ('src/api') {
                script {
                     bat 'npm install'
                }
              } */
        }
        stage('Build Image') {
            steps {
              dir ('src/web') {
                script {
                     docker.build registry + ":v$BUILD_NUMBER"
                     dockerImage_web = docker.build registry + "/node-web-app:v$BUILD_NUMBER"
                }
              }
             /*  dir ('src/api') {
                script {
                     docker.build registry + ":v$BUILD_NUMBER"
                     dockerImage_api = docker.build registry +"/node-api-app:v$BUILD_NUMBER"
                }
              } */
            }
        }
        stage('Push Image') {
            steps {
              script {
                 docker.withRegistry( '', registryCredential ) {
                 dockerImage_web.push()
                 //dockerImage_api.push()
                }
              }
            }
        }
        stage('Deploy Prod') {
            steps {
                  git(credentialsId: '1bd4fb12-1bd4-4f3f-b155-7764792770ab', url: 'https://github.com/DaviAraujoCC/K8s-CICD', branch: 'main')
                 // bat "cd ./prod && kustomize edit set image david13356/node-api-app=david13356/node-api-app:v$BUILD_NUMBER"
                  bat "cd ./prod && kustomize edit set image david13356/node-web-app=david13356/node-web-app:v$BUILD_NUMBER"
                  bat "git add ./prod"
                  bat "git commit -am \"Publish new version $BUILD_NUMBER\" && git push -f origin main"
          }
        }
        stage('Remove Unused docker image') {
           steps{
            // bat "docker rmi $registry/node-api-app:v$BUILD_NUMBER"
             bat "docker rmi $registry/node-web-app:v$BUILD_NUMBER"
           }
        }
    }
}
