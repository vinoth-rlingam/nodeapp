pipeline {
    agent any
    environment{
        registry ="vinothrlingam/nodeapp"
        registryCredential ='dockerhub'
        dockerImage =''
    }
      stages{
        stage('git clone'){
            steps{
                git 'https://github.com/vinoth-rlingam/nodeapp.git'
            }
        }
         stage('Install Dependencies'){
            steps{
                sh 'npm install'
            }
        }
        stage('Build docker Image'){
            steps{
                script{
                    dockerImage =docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }

       stage ('Deploy docker Image')  {
           steps{
               script{
                   docker.withRegistry('', registryCredential){
                       dockerImage.push()
                   }
               }
           }
       }
       stage('remove unused images'){
          steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
          }
       }

    }

}
