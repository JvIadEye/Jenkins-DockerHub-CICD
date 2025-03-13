pipeline {
  agent any

  //get the credential of dockerhub from jenkins
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  
  stages {
    //building image
    stage('Build') {
      steps {
        sh 'docker build -t jviadeye/nginx_image .'
        nexusPolicyEvaluation advancedProperties: '', callflow: [enable: false], enableDebugLogging: false, failBuildOnNetworkError: false, failBuildOnScanningErrors: false, iqApplication: selectedApplication('sandbox-application'), iqInstanceId: 'iq', iqOrganization: '3ceec037027b4f329d862b9d8d75b5ef', iqScanPatterns: [[scanPattern: '']], iqStage: 'build', jobCredentialsId: '', unstableBuildOnScanningWarnings: false
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
