pipeline {
    agent any
        environment{
            REPOSITORY_NAME = "ansible_folder"
            SSH_KEY = credentials('SSH_KEY')

        }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
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
