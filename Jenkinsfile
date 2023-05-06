pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'main', url: 'https://github.com/gabrielagherman/calculator-servlet-example.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps { 
	      //sh ' docker socket'              
		sh 'docker build -t calculator:latest .' 
                sh 'docker tag calculator gabrielagherman/calculator:latest'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "docker-cred", url: "" ]) {
          sh  'docker push gabrielagherman/calculator:latest'
        }
                  
          }
        }
     
      // stage('Run Docker container on Jenkins Agent') {
             
          //   steps 
			//{
          //   sh "docker run -d -p 8003:8080 gabrielagherman/calculator"
 
           // }
        // }
 
	// stage("Git Checkout"){
	//	 steps{
	//		 sh 'pwd'
	//		 sh 'git clone https://github.com/gabrielagherman/calculator-servlet-example.git'
	//	 	 sh 'pwd'
	//	 }
	 //}
	 stage ("Run ansible playbook on remote hosts")
	 {
		 steps{
			sh 'cd /etc/ansible'
			sh 'pwd'
			sh 'chmod aws key' 
			sh 'ansible-playbook ./calculator-servlet-example/playbook.yaml -i ./calculator-servlet-example/inventory --key-file ./calculator-servlet-example/aws-key.pem'
		 }
	 }

	}
}
