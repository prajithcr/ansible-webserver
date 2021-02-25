pipeline {
    agent { label "agentfarm" }
    stages {
        stage('Delete the workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Installing Ansible') {
            steps {
                script {
                    def ansible_exists = fileExists '/usr/bin/ansible'
                    if (ansible_exists == true) {
                        echo " Skipping Ansible Install - allready installed"

                    } else {
                        sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
                        sh 'sudo apt nstall -y wget tree unzip ansible python3-apt'
                    }
                }
            }
        }
        stage('Download Ansible Code') {
            steps {
                git credentialsId: 'git-repo-cred', url: 'git@github.com:prajithcr/ansible-webserver.git'
                echo "Third stage"
            }
        }
        stage('Run Ansible-lint against playbok') {
            steps {
                sh 'id'
                sh 'docker run --rm -v $WORKSPACEplaybooks:/data cytopia/ansible-lint apache-install.yml'
                sh 'docker run --rm -v $WORKSPACE/playbooks:/data cytopia/ansible-lint apache-update.yml'
                sh 'docker run --rm -v $WORKSPACE/playbooks:/data cytopia/ansible-lint apache-test.yml'
                sh ' echo my newtest11"}
        }
    }

}

