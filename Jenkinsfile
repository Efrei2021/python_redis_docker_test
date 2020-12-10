pipeline {
  agent any
  stages{
    stage('Build'){
      echo 'Building the docker image'
      sh 'docker build -t myApp .'
    }
    stage('Run'){
      paralle1{
        stage('Run redis'){
          sh 'docker run -d -p 6376:6376 --name myredis redis'
          
        }
        stage('Run flask'){
          sh 'docker run --name myApp_c -d -p 5000:5000 myApp'
          
        }
      }
    }
    stage('Build'){
      echo 'Building the docker image'
      sh 'docker build -t myApp .'
    }
    stage('Testing'){
      steps{
        sh 'python test_app.py'
      }
    }
    stage('Stop container'){
      stage{
        steps{
          sh 'docker rm -f myApp_c'
          sh 'docker rm -f myredis '
        }
      }
    }
  }
}
