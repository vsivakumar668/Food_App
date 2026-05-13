pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET = 'clahantech2026'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/vsivakumar668/Food_App.git'
            }
        }

        stage('Verify Files') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Deploy to S3') {
            steps {

                withAWS(credentials: 'aws-credentials', region: 'us-east-1') {

                    sh '''
                    aws s3 sync . s3://$S3_BUCKET --delete \
                      --exclude ".git/*" \
                      --exclude "Jenkinsfile"
                    '''

                }
            }
        }
    }

    post {

        success {
            echo 'Website deployed successfully to S3'
        }

        failure {
            echo 'Pipeline failed'
        }
    }
}
