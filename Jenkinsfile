pipeline {
    agent any

    environment {
        DEV_SERVER = "13.60.162.63"
        STG_SERVER = "13.60.192.22"
        PRD_SERVER = "13.60.157.132"
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
