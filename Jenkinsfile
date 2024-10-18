pipeline {
  agent any

  //get the credential of dockerhub from jenkins
  environment {
    DOCKERHUB_CREDENTIALS = credentials('Credentials for Dockerhub')
  }
  
  stages {
    //building image
    stage('Build') {
      steps {
        sh 'docker build -t jviadeye/nginx_image .'
      }
    }


    //publish image on dockerhub
    stage('Publish') {
      steps {
        sh '''
          docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW
          docker push jviadeye/nginx_image
          docker logout
        '''
      }
    }
  }
}
