node {
   stage('Preparation') { 
      git 'https://github.com/karthik-tp/positiontracking'
   }
   stage('Build') {
  
         sh "mvn clean package"
      
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
   stage('Deploy')
   {
     withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) 
     {
         ansiblePlaybook credentialsId: 'ssh-agent', playbook: 'deploy.yaml', sudo: true, sudoUser: null
     }
   }
}
