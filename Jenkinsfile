pipeline {
    agent {
        label 'ansible'
    }

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/sonaliankushe55-cell/aws-ansible-Jenkins-project.git'
            }
        }

        stage('Install Python Dependencies') {
            steps {
                sh 'pip3 install boto3 botocore'
            }
        }

        stage('Install Ansible Collection') {
            steps {
                sh 'ansible-galaxy collection install amazon.aws'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh 'ansible-playbook playbook.yml'
            }
        }
    }
}
