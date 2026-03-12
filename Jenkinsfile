pipeline {
    agent any

    environment {
        DEV_SERVER = "DEV_EC2_PUBLIC_IP"
        STG_SERVER = "STG_EC2_PUBLIC_IP"
        PRD_SERVER = "PRD_EC2_PUBLIC_IP"
        USER = "ec2-user"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Apache') {
            steps {
                sh '''
                sudo yum install httpd -y
                sudo systemctl start httpd
                sudo systemctl enable httpd
                '''
            }
        }

        stage('Deploy to DEV') {
            when {
                branch 'dev'
            }
            steps {
                sh '''
                sudo cp index.html /var/www/html/index.html
                sudo systemctl restart httpd
                '''
            }
        }

        stage('Deploy to STG') {
            when {
                branch 'stg'
            }
            steps {
                sh '''
                sudo cp index.html /var/www/html/index.html
                sudo systemctl restart httpd
                '''
            }
        }

        stage('Deploy to PROD') {
            when {
                branch 'main'
            }
            steps {
                sh '''
                sudo cp index.html /var/www/html/index.html
                sudo systemctl restart httpd
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Successful"
        }

        failure {
            echo "Deployment Failed"
        }
    }
}
