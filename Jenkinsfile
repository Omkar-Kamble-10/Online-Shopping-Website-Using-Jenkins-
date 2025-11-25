pipeline {
    agent any

    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from the same GitHub repo where the Jenkins job is configured
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Static HTML/CSS project – nothing to compile.'
            }
        }

        stage('Test') {
            steps {
                // Simple placeholder step; in real projects you could run HTML/CSS linters here
                echo 'No automated tests configured yet.'
            }
        }

        stage('Package') {
            steps {
                script {
                    sh 'mkdir -p dist'
                    sh 'cp -r index.html about.html assets dist/'
                    sh 'cd dist && zip -r site-artifact.zip .'
                }
            }
        }

        stage('Deploy') {
            when {
                expression { return env.DEPLOY_PATH != null && env.DEPLOY_PATH != '' }
            }
            steps {
                // Change DEPLOY_PATH in Jenkins job configuration (environment variable)
                // Example: /var/www/html/my-site
                sh '''
                    echo "Deploying to: $DEPLOY_PATH"
                    rsync -av --delete dist/ "$DEPLOY_PATH"/
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
