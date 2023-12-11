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
        cleanWs()
        checkout scm
      }
    }
    stage('verify tools'){
     steps{
       sh '''
        docker info
        docker version
        docker-compose version
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
            docker-compose build
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
           docker-compose up -d
        '''
      }
    }
    stage('Check Container'){
      steps{
        sh '''
           docker ps -a
           docker images
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