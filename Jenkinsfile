#!groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[url: 'https://github.com/Mezraniwassim/spring-boot-microservices.git']]
                    ])
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    dir('/home/wassim/Desktop/project/spring-boot-microservices') { // Change this to the correct path
                        sh 'mvn package'
                    }
                }
            }
        }
        stage('Dockerize') {
            steps {
                script {
                    // List of microservices
                    def services = [
                        'eureka-service',
                        'config-service',
                        'gateway-service',
                        'auth-service',
                        'user-service',
                        'job-service',
                        'notification-service',
                        'file-storage-service'
                    ]

                    dockerizeAndPushImages(services)
                }
            }
        }
    }
}

def dockerizeAndPushImages(services) {
    for (service in services) {
        sh """
        cd ${service}
        docker build -t mezrani/spring/${service}:latest .
        docker push mezrani/spring/${service}:latest
        cd ..
        """
    }
}