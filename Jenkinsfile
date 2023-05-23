pipeline {
    agent any 	
	environment {
		
		PROJECT_ID = 'sit737'
                CLUSTER_NAME = 'sit737-cluster-node'
                LOCATION = 'australia-southeast1'
                CREDENTIALS_ID = 'gcp_cred'		
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
       stage('Initialize'){
        def dockerHome = tool 'myDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
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
                      docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                      myimage.push("${env.BUILD_ID}")
                     }   
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