pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
        stage('Dockerize') {
            steps {
                script {
                    // List of microservices
                    def services = ['auth-service', 'user-service', 'job-service', 'notification-service', 'file-storage-service']

                    for (service in services) {
                        sh """
                        cd ${service}
                        docker build -t mezrani/spring/${service}:latest .
                        docker push mezrani/spring/${service}:latest
                        cd ..
                        """
                    }
                }
            }
        }
    }
}
