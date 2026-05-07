pipeline {
    agent any

    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }

    tools {
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vinay-cs245/MavenAnsibleWebApp1'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh 'ls -R'   // DEBUG step (remove later)

                sh 'ansible-playbook $WORKSPACE/ansible/playbook.yml -i $WORKSPACE/ansible/hosts.ini'
            }
        }
    }
}
