pipeline{
  agent{
    node{
      label '410977012'
    }
  }
  environment{
    DOCKERHUB_CREDENTIALS = credentials('410977012-dockerhub')
  }
  options {
      skipDefaultCheckout(true)
  }
  stages{
    stage('Clean old DOCs & chekcout SCM'){
      steps{
        // two critical functions
      }
    }
    stage('verify tools'){
     steps{
       sh '''
       // your command
       '''
     }  
    }
    stage('Login Dockerhub'){
      steps{
        sh '''
          echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
        '''
      }
    }
    stage('Build image for application'){
      steps{
        sh '''
          // your command
        '''
      }
    }
    stage('Rename && Push image to Dockerhub'){
      steps{
        sh '''
          docker tag  410977012_1211_ci4_service:v0.1 linweihsuan/410977012_1211_ci4_service:v0.1
          docker push linweihsuan/410977012_1211_ci4_service:v0.1
        '''
      }
    }
    stage('Start Container'){
      steps{
        sh '''
           // your command
        '''
      }
    }
    stage('Check Container'){
      steps{
        sh '''
           // your command
        '''
      }
    }
   }
   post {
        always {
          sh '''
          docker-compose down
          docker system prune -a -f
          docker logout
          '''
        }
      }
}
