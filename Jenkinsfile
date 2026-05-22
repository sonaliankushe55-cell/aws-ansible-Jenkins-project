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

        stage('Setup Python Virtual Environment') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install boto3 botocore ansible
                '''
            }
        }

        stage('Install Ansible Collection') {
            steps {
                sh '''
                . venv/bin/activate
                ansible-galaxy collection install amazon.aws
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                . venv/bin/activate
                ansible-playbook create_ec2.yml
                '''
            }
        }
    }
}
