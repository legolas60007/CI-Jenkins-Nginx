pipeline {
	agent any
	
	environment {
		dockerfilePath= "/opt/jenkins/"
		registry = "legos60007/jenkinstest1:v1"
		registryCredential = 'dockerhub'
	}
	stages {
		stage ('Test') {
			steps {
				sh 'echo executing test'
			}
		}
        stage ('Build Docker') {
			steps {
				script {
					dockerImage = docker.build(registry, "-f ${dockerfilePath}Dockerfile .")
				}
			}
		}
		stage ('Push Docker') {
			steps {
				script {
					docker.withRegistry('', registryCredential){
						dockerImage.push()
					}
				}
			}
		}
		stage ('Run Docker'){
			steps{
				sh 'docker run -d -p 1500:80 ${registry}'
			}
		}
	}
}
