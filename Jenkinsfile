pipeline {
  agent any
  
  environment {
  
  SERVICE_NAME = "liquid07/website-php"
  REPOSITORY_TAG="${YOUR_DOCKERHUB_USERNAME}/${ORGANIZATION_NAME}-${SERVICE_NAME}:${BUILD_ID}"
  }
  
  stages{
     stages('Preparation'){
        steps {
           cleanWs()
           
           git credentialsId: 'GIT_HUB_CREDENTIALS', url: "https://github.com/patiwat13/patiwat13.git"
        }
     
     }
    
  }
  
}
