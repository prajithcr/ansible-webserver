pipeline {
    agent { label "agentfarm" }
    environment {
        KEY_FILE = '/home/elon/.ssh/vm-instance-key'
        USER = 'elon'
    }
    stages {
        stage('Delete the workspace') {
            steps {
                cleanWs()
            }
        }
        
        stage('Install Apache &Upload website') {
            steps {
              sh 'ansible-playbook -u $USER --private-key $KEY_FILE -i $WORKSPACE/host_inventory $WORKSPACE/playbooks/apache-install.yml'
              sh 'ansible-playbook -u $USER --private-key $KEY_FILE -i $WORKSPACE/host_inventory $WORKSPACE/playbooks/website-update.yml'
            }
        }
        stage('Test Website') {
            steps {
              sh 'ansible-playbook -u $USER --private-key $KEY_FILE -i $WORKSPACE/host_inventory $WORKSPACE/playbooks/apache-test.yml'
            }
        }
    }
}

