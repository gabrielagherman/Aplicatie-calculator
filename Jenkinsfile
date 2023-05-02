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
			{
          //   sh "docker run -d -p 8003:8080 gabrielagherman/calculator"
 
           // }
        // }
 
	 stage("Git Checkout"){
		 steps{
			 sh 'pwd'
			 sh 'git clone https://github.com/gabrielagherman/calculator-servlet-example.git'
		 	 sh 'pwd'
		 }
	 }
	 stage ("Run ansible playbook on remote hosts")
	 {
		 steps{
			//sh 'cd /var/lib/jenkins/workspace/auto-deploy/aplicatie-de'
			sh 'cd /etc/ansible'
			sh 'pwd'
			//ansiblePlaybook (credentialsId: 'credentialeptmasina', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/var/lib/jenkins/workspace/auto-deploy/application-deployment/inventory', playbook: '/var/lib/jenkins/workspace/auto-deploy/application-deployment/playbook.yaml')
		 	//ansiblePlaybook credentialsId: 'credentialeptmasina', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/var/lib/jenkins/workspace/auto-deploy/application-deployment/inventory', playbook: '/var/lib/jenkins/workspace/auto-deploy/application-deployment/playbook.yaml'
			sh 'ansible-playbook ./calculator-servlet-example/playbook.yaml -i ./calculator-servlet-example/inventory --key-file ./calculator-servlet-example/aws-key.pem'
			 //ansiblePlaybook credentialsId: 'credentialeptmasina', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/etc/ansible/inventory', playbook: '/etc/ansible/playbooktest.yaml'
		 }
	 }
	 
	 
	 
 // stage('Run Docker container on remote hosts') {
             
   //         steps {
		//withAWS(credentials: 'credentiale-masina', region: 'eu-central-1'){
		//sshagent(['credentials']) {
		   // sh "ssh -tt ubuntu@3.71.176.233" 
	//	    sh "ssh ubuntu@3.71.176.233 docker run -d -p 8003:8080 gabrielagherman/samplewebapp"
		   
		   // sh "docker run -d -p 8003:8080 gabrielagherman/samplewebapp"
		//}
            //}
        
   // }
	}
}
