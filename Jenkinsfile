pipeline {
    agent any
    stages {
              stage("Install zabbix server") {
             // agent any
                   when {
                      expression { GIT_BRANCH == 'origin/master' }
                   }
                   steps {
                       sh 'ansible-playbook -i hosts  zabbix_playbook.yml'
                   }
               }
    }
}
