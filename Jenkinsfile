pipeline {
    agent any
    stages {
        
        stage('Prepare ansible environment') {
        //    agent any
            environment {
               // VAULTKEY = credentials('vaultkey')
                DEVOPSKEY = credentials('devopskey')
            }
            steps {
              //  sh 'echo \$VAULTKEY > vault.key'
                sh 'cp \$DEVOPSKEY id_rsa'
                sh 'chmod 600 id_rsa'
            }
         }
        
             stage("Install ansible role dependencies") {
            agent any
                   steps {
                       sh 'ansible-galaxy install  -r roles/requirements.yml'
                   }
               }

        
              stage("Install zabbix server") {
             // agent any
                   when {
                      expression { GIT_BRANCH == 'origin/master' }
                   }
                   steps {
                        sh 'ansible-playbook -i hosts  --private-key id_rsa  zabbix_playbook.yml'
                   }
               }
    }
}
