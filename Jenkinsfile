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

                withCredentials([usernamePassword(
                    credentialsId: 'aws-creds',
                    usernameVariable: 'AWS_ACCESS_KEY_ID',
                    passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                )]) {

                    sh '''
                    . venv/bin/activate

                    export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                    export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

                    ansible-playbook -i localhost, create_ec2.yml
                    '''
                }
            }
        }
    }
}
