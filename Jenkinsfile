pipeline {
   agent any

   environment {
     // You must set the following environment variables
     // ORGANIZATION_NAME
     // YOUR_DOCKERHUB_USERNAME (it doesn't matter if you don't have one)

     SERVICE_NAME = "helloworld"
     //REPOSITORY_TAG="minikube/aubriellepie-comfortT-${SERVICE_NAME}:${BUILD_ID}"
     REPOSITORY_TAG="https://github.com/aubriellepie-comfortT/fleetman-webapp.git"
   }

   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'GitHub', url: "https://github.com/aubriellepie-comfortT/helloworld.git"
         }
      }
      stage('Build') {
         steps {
            bat '''mvn clean package'''
         }
      }

      stage('Build and Push Image') {
         steps {
           bat 'docker image build -t ${REPOSITORY_TAG} .'
         }
      }

      stage('Deploy to Cluster') {
          steps {
                    bat 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl apply -f -'
          }
      }
   }
}
