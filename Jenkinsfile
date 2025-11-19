pipeline {
    agent any

    tools {
        maven 'Maven-3.9.9'
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/bhargavisirigiri/maven-pro.git', branch: 'main'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy(
                    adapters: [
                        tomcat9(
                            credentialsId: 'tomcat-deploy',
                            path: '',
                            url: 'http://44.255.197.58:8080'
                        )
                    ],
                    war: 'target/*.war'
                )
            }
        }
    }
}

