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
        stage('Third Stage') {
            steps {
                echo "Third stage"
            }
        }
    }

}
