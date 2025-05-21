pipeline {
    agent { label 'dind' }

    stages {
        stage('Build') {
            steps {
                echo 'Building on a labeled node...'
                // Insert your build steps here
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Insert your test steps here
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Insert your deploy steps here
            }
        }
    }
}
