pipeline {
    agent any
        environment{
            REPOSITORY_NAME = "ansible_folder"
            EC2_INSTANCE = "3.249.109.95"
            SSH_KEY = credentials('SSH_KEY')

        }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh 'ansible --version'
            }
        }
        stage ('Use Ansible to provision Docker and folders') {
            steps {
            echo 'Dynamically provisioning Docker into AWS Machines'
                sh """
                ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i ansible_hosts --key-file ${SSH_KEY} playbooks/02-docker.yml -u ec2-user
                ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i ansible_hosts --key-file ${SSH_KEY} playbooks/01-dir.yml -u ec2-user
                """
            }
        }
    } 
    post {
        always {
            echo 'Always Post'
            deleteDir()
        }
    }
}
