pipeline {
	agent any
	tools {
		maven "maven-3.9.9"
		jdk "java-17"
	}
	stages {
		stage('Clone'){
			steps {
			    git url: "https://github.com/bharathdevust/service-registry.git",
			    branch: "master"
			}
		}
		stage('Build'){
		    steps {
			    bat "mvn clean install -DskipTests"
			}
		}
		stage('Test'){
			steps {
			    bat "mvn test"
            }
		}
		stage('Deploy') {
			steps {
			    bat "docker rm -f service-register"
			    bat "docker rmi -f service-image"
			    bat "docker build -t service-image ."
                bat "docker run -p 8090:8090 -d --name service-register service-image"
            }
		}
	}
}
