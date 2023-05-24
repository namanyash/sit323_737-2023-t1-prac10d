pipeline {
    agent any 	
	environment {
		
		PROJECT_ID = 'sit737'
                CLUSTER_NAME = 'sit737-cicd-cluster'
                LOCATION = 'us-east1-d'
                CREDENTIALS_ID = 'kubernetes'		
	}
    stages {	
      stage('Scm checkout') {
         steps{
            checkout scm
         }
      }
	   stage('Test') { 
		steps {
	         echo "Testing..."
            //do some tests
            sleep(time:3,unit:"SECONDS")
            echo "Success"
		}
	   }
	   stage('Build Docker Image') { 
		steps {
		   sh 'whoami'
                   script {
		      myimage = docker.build("namanyash/sit737-ci-cd:${env.BUILD_ID}")
                   }
                }
	   }
	   stage("Push Docker Image") {
                steps {
                   script {
                     echo "Push Docker Image"
                     withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                              sh "docker login -u namanyash -p ${dockerhub}"
                     }
                        myimage.push("${env.BUILD_ID}")
                     
                  }
                }
            }
	   
           stage('Deploy to K8s') { 
                steps{
                   echo "Deployment started ..."
		   sh 'ls -ltr'
		   sh 'pwd'
		   sh "sed -i 's/tagversion/${env.BUILD_ID}/g' deployment.yaml"
                   step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
		   echo "Deployment Finished ..."
            }
	   }
       
    }
}