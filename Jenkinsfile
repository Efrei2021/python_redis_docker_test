pipeline{
	agent any
	stages{
		stage('Build'){
			echo 'Building the docker images'
			sh 'docker build -t myflaskapp .'
		}
		parallel{
			stage('run redis'){
				steps{
					sh 'docker run -d -p 6379:6379 --name myredis redis'
				}
			}
			stage('run flask'){
				steps{
					sh 'docker run -d -p 5000:5000 --name myflaskapp_c myflaskapp'
				}
			}
		}
		stage('Testing'){
			steps{
				sh 'python3 test_app.py'
			}
		}
		stage('stop container'){
			steps{
				sh 'docker rm -f myflaskapp_c'
				sh 'docker rm -f redis'
			}
		}
	}
}
