pipeline {
	agent any
	environment {
		DOCKER_LOGIN=credentials('DOCKER_LOGIN')
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
				sh 'docker stop app1'
				sh 'docker rm app1'
				sh 'dockerbuild -t marSanGal/app1'
				sh 'docker login -u ${DOCKER_LOGIN_USR} -p ${DOCKER_LOGIN_PSW}'
				sh 'docker push marSanGal/app1'
			}
		}
		stage('Deploy') {
			steps {
				sh 'echo hello >> example.txt'
			}
		}
	}
}