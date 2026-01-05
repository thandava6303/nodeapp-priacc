pipeline {
    agent any
      tools {
  nodejs 'node'
}
triggers {
  pollSCM '* * * * *'
} 
    stages {
        stage('check the code from scm') {
            steps {
                git branch: 'main', url: 'https://github.com/thandava6303/nodeapp-priacc.git'
            }
        }
        stage('install npm dependices') {
            steps {
                sh'npm install'
            }
        }
        stage('build docker image') {
            steps {
                sh'docker build -t thandava/newnodeapp-1 .'
            }
        }
        stage("Docker Push"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'docker_password', usernameVariable: 'docker_user')]) {
                    sh "docker login -u ${docker_user} -p ${docker_password}"
                }
                sh "docker push thandava/newnodeapp-1"
                
            }
        } 
        stage('build docker container') {
            steps {
                sh'docker stop krishnacontainer'
                sh'docker rm krishnacontainer'
                sh'docker run -d -p 3000:3000 --name krishnacontainer thandava/newnodeapp-1'
            }
        }
      

    }
post {
    success {
        mail to: 'kaluvalathandavakrishna@priaccinnovations.ai',
             subject: "Build SUCCESS: ${env.JOB_NAME}",
             body: "Build ${env.BUILD_NUMBER} succeeded."
    }
    failure {
        mail to: 'kaluvalathandavakrishna@priaccinnovations.ai',
             subject: "Build FAILED: ${env.JOB_NAME}",
             body: "Please check Jenkins console output."
    }
}
}
