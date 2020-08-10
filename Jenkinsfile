pipeline {
    agent any
    stages {
        
        stage('Prepare ansible environment') {
    
            environment {
  
                DEVOPSKEY = credentials('devopskey')
            }
            steps {
              //  sh 'echo \$VAULTKEY > vault.key'
                sh 'cp \$DEVOPSKEY id_rsa'
                sh 'chmod 600 id_rsa'
            }
         }
        
        
              stage("Install zabbix server") {
      
                   when {
                      expression { GIT_BRANCH == 'origin/master' }
                   }
                   steps {
                        sh 'ansible-playbook -i hosts  --private-key id_rsa  zabbix_playbook.yml'
                   }
               }
    }
}
