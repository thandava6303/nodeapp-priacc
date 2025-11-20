pipeline {
    agent any


    stages {

        stage('Clone Repository') {
            steps {
             git branch: 'main', url: 'https://github.com/thandava6303/nodeapp-priacc.git'            }
        }

        stage('Check Required Tools') {
           steps {
                echo 'Checking Docker version...'
                sh 'docker --version'
                
                echo 'Checking unzip version...'
                sh 'unzip -v'
            }
        }

        stage('Unzip Source Code') {
            steps {
                // unzip your code here
            }
        }

        stage('Navigate & List Files') {
            steps {
                // cd into main folder
                // list files
            }
        }

        stage('Docker Build Image') {
             steps {
                script {
                    // Build a Docker image from a Dockerfile
                    docker.build('my-app-image:latest')
                }
            }

        stage('Docker Run Container') {
            steps {
                script {
                    // Run a Docker container
                    docker.image('my-app-image:latest').run('-p 8080:8080')
                }
            }

    }
}

