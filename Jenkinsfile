pipeline {
    agent any

    tools {
        maven 'maven'
    }

    environment {
        TOMCAT_USER = "admin"
        TOMCAT_PASS = "admin123"
        TOMCAT_URL  = "http://<34.222.239.150>:8080/manager/text"
    }

    stages {
        
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bhargavisirigiri/maven-pro.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                    WAR_FILE=$(ls target/*.war)
                    echo "Deploying WAR: $WAR_FILE"

                    curl -u $TOMCAT_USER:$TOMCAT_PASS \
                        -T $WAR_FILE \
                        "$TOMCAT_URL/deploy?path=/myapp&update=true"
                '''
            }
        }
    }
}
