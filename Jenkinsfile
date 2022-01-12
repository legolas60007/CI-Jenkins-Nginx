pipeline {
	agent any
	
	environment {
		dockerfilePath= "/opt/jenkins1/"
		registry = "legos60007/app_for_demo:v1"
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
				sh 'docker run -d -p 25400:80 ${registry}'
			}
		}
	}
}
