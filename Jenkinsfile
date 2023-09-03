pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
                git 'https://github.com/Saish40/website-CICD.git'
            }
        }
        stage('Build Image') {
            steps {
                sh "docker build -t saish40/web ."
            }
        }
        stage('Docker login and push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerpwd', usernameVariable: 'dockerusr')]) {
                sh "docker login -u ${env.dockerusr} -p ${env.dockerpwd}"
                }
                sh "docker push saish40/web:latest"
            }
        }
        stage('Deploying container') {
            steps {
                sh "docker run -d --name website -p 80:80 saish40/web:latest"
            }
        }
    }
}
