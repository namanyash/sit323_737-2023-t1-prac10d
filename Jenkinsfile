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
	       stage('Build image') {
       dockerImage = docker.build("namanyash/test:v1")
    }
    
      stage('Push image') {
            withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
            dockerImage.push()
            }
         }                            
            
    }
}