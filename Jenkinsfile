pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET = 'clahantech2026'
    }

    stages {

        stage('Clone GitHub Repo') {
            steps {
                git 'https://github.com/vsivakumar668/Food_App.git'
            }
        }

        stage('List Files') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Upload Website to S3') {
            steps {
                sh '''
                aws s3 sync . s3://$S3_BUCKET --delete \
                  --exclude ".git/*" \
                  --exclude "Jenkinsfile"
                '''
            }
        }
    }

    post {
        success {
            echo 'Website uploaded successfully to S3'
        }

        failure {
            echo 'Pipeline failed'
        }
    }
}
     



      
