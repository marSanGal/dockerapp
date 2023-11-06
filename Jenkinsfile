pipeline {
	agent any
	environment {
		DOCKER_LOGIN=credentials('DOCKER_LOGIN')
		DATABASE_URI=credentials()
	}
	stages { 
		stage('Test') {
			steps {
				sh 'docker build -t app1 .'
				sh 'docker run -d -p 5000:5000 --name app1 app1'
			}
		}
		stage('Build') {
			steps {
				sh 'docker stop dockerapp/app1'
				sh 'docker rm dockerapp/app1'
				sh 'dockerbuild -t dockerapp/app1'
				sh 'docker login -u ${DOCKER_LOGIN_USR} -p ${DOCKER_LOGIN_PSW}'
				sh 'docker push dockerapp/app1'
			}
		}
		stage('Deploy') {
			steps {
				sh 'echo hello >> example.txt'
			}
		}
	}
}