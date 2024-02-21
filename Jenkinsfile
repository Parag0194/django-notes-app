pipeline {
    agent any

    stages {
        stage('Code Clone') {
            steps {
                echo 'cloning the code'
                git url:"https://github.com/Parag0194/django-notes-app.git", branch: "main"
            }
        }
        stage('build') {
            steps {
                echo 'building the image'
                sh "docker build -t my-notes-app ."
            }
        }
        stage('push to dockerhub') {
            steps {
                echo 'pushing the image to dockerhub'
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubuser")]){
                sh "docker tag my-notes-app ${env.dockerhubuser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubPass}"
                sh "docker push ${env.dockerhubuser}/my-notes-app:latest"
                }
            }
        }
        stage('deploy') {
            steps {
                echo 'deploying the container'
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
        
    }
}
