node {
   stage('Preparation') { 
      git 'https://github.com/karthik-tp/positiontracking'
   }
   stage('Build') {
  
         sh "mvn package"
      
   }
   stage('Results') {
      archive 'target/*.jar'
   }
   stage('Deploy')
   {
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'awscredentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) 
	  {
		ansiblePlaybook credentialsId: 'ssh-privateKey', installation: 'ansible-installation-path', playbook: 'deploy.yaml', sudoUser: null
          }
   }
}
