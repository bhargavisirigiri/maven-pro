pipeline {
    agent any

    tools {
        maven 'maven'   // Jenkins Maven installation name
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/bhargavisirigiri/maven-pro.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-deploy',
                        path: '',
                        url: 'http://44.255.197.58:8080'
                    )
                ], 
                war: 'target/*.war'
            }
        }
    }
}

