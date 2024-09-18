pipeline {
    agent any {
        tools {
            maven 'maven3'
            jdk 'jdk8'
        }
    }
    stages {
        stage('Build Maven') {
            steps {
                sh 'pwd'
                sh 'mvn clean install package'
            }
        }
        stage('Copy Artifact') {
            steps {
                sh 'pwd'
                sh 'cp -r target/*.jar docker'
            }
        }
        stage('Build Docker image') {
            steps {
                script {
                    def customImage = docker.build('initsixcloud/petclinic', "./docker")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    {
                        customImage.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }
    }
}
