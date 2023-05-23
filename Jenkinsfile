pipeline {
    agent any 	
	environment {
		
		PROJECT_ID = 'sit737'
                CLUSTER_NAME = 'sit737-cluster-node'
                LOCATION = 'australia-southeast1'
                CREDENTIALS_ID = 'gcp_cred'		
                DOCKERHUB_CREDENTIALS = credentials('dockerhub')
	}
    stages {	
	   stage('Test') { 
		steps {
	         echo "Testing..."
            //do some tests
            sleep(time:3,unit:"SECONDS")
            echo "Success"
		}
	   }
         stage('build'){  steps {  sh "docker build -t namanyash/sit737-ci-cd:${env.BUILD_ID} ."  -v "$(which docker):/usr/bin/docker"  -v "/var/run/docker.sock:/var/run/docker.sock" -v "$(which docker):/usr/bin/docker" -v "jenkins_home:/var/jenkins_home jenkins/jenkins:lts" }  }
         stage('Login'){  steps {  sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin ' }}
         stage('Push'){  steps {  sh "docker push tfkben/ben:latest"}   }       
    }
}