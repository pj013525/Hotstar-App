pipeline {
    agent any

    stages {
        stage('Git  Checkout') {
            steps {
               git 'https://github.com/pj013525/Hotstar-App.git'
            }
        }
        stage('Compiling') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Packing') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Deploying To Tomcat') {
            steps {
                sh 'docker build -t pj013525/tomcat-image:v1 .'
                sh 'docker images'
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-details', variable: 'dockerhubPassword')]) {
                    sh "docker login -u pj013525 -p ${dockerhubPassword}"
                    sh 'docker push pj013525/tomcat-image:v1'
                } 
            }
        }    
        stage('Docker Container') {
            steps {
                    sh 'docker run -dt --name hotstarapp -p 9000:9000 pj013525/tomcat-image:v1'
            }
        }  
    }
}
