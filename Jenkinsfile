pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Jaydeepc1985/elearn-frontend.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'ls -l' // <-- debug: show contents
                sh 'docker build -t Jaydeepc1985/elearn-frontend .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '''
                        echo $PASSWORD | docker login -u $USERNAME --password-stdin
                        docker push Jaydeepc1985/elearn-frontend
                    '''
                }
            }
        }

        stage('Deploy on App Server') {
            steps {
                echo 'Deployment step goes here...'
            }
        }
    }
}
