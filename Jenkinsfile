pipeline {
    agent none

    stages {
        stage('Checkout') {
            agent { label 'dind' }
            steps {
                sh 'ls -lanh'
            }
        }
        stage('Build') {
            agent { label 'dind' }
            steps {
                sh 'docker build . -t supercoolaccount/pokemon-app:latest'
                sh 'docker build . -t pytest -f test.Dockerfile'
            }
        }

        stage('Test') {
            agent { label 'dind' }
            steps {
                sh 'docker build -t test-pokedex -f test.Dockerfile .'
                sh 'docker run test-pokedex'
            }
        }

        stage('Push') {
            agent { label 'dind' }
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    """
                }
                echo 'push application...'
                sh "docker push supercoolaccount/pokemon-app:latest"
            }
        }
        stage('Deploy') {
            agent { label 'cloud_agent' }
            steps {
                sh 'sudo docker run -d -p 5000:5000 supercoolaccount/pokemon-app:latest'
            }
        }
    }
}
