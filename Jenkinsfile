pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Let\'s build  the image'
        sh 'docker build -t myflaskapp:0.2 .'
      }
    }

    stage('Run containers') {
      parallel {
        stage('Run containers') {
          steps {
            echo 'run containers'
            sh 'docker run -d -p 6379:6379 --name myredis redis:alpine '
          }
        }

        stage('Fask') {
          steps {
            sh 'docker run -d -p 5000:5000 --name myflaskapp_c myflaskapp:0.2'
          }
        }

      }
    }

    stage('Testing') {
      steps {
        echo 'Testing'
        sh 'python3 test_app.py'
      }
    }

    stage('FInal') {
      steps {
        echo 'remove containers'
        sh 'docker container rm -f $(docker container ls -qa)'
      }
    }

  }
}