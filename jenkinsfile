pipeline {
    agent any
    tools {
        maven 'maven_3_5_0'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scm: [$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sanaabahcine/spring-petclinic']]]
                sh 'mvn clean install'
            }
        }
        stage('Build docker image') {
            steps {
                script {
                    app = docker.build("sanaeabahcine371/spring-petclinic")
                }
            }
        }
        stage('Push image to dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }
       
    }
}
