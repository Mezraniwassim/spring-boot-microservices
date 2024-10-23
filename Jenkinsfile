pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Mezraniwassim/spring-boot-microservices.git', 
                    branch: 'main'
            }
        }

        stage('Build Microservices') {
            parallel {
                stage('Build Eureka Server') {
                    steps {
                        dir('eureka-server') {
                            sh 'mvn clean install -DskipTests'
                        }
                    }
                }

                stage('Build Gateway') {
                    steps {
                        dir('gateway') {
                            sh 'mvn clean install -DskipTests'
                        }
                    }
                }

                stage('Build Config Server') {
                    steps {
                        dir('config-server') {
                            sh 'mvn clean install -DskipTests'
                        }
                    }
                }

                stage('Build Auth Service') {
                    steps {
                        dir('auth-service') {
                            sh 'mvn clean install -DskipTests'
                        }
                    }
                }

                stage('Build User Service') {
                    steps {
                        dir('user-service') {
                            sh 'mvn clean install -DskipTests'
                        }
                    }
                }

                stage('Build Job Service') {
                    steps {
                        dir('job-service') {
                            sh 'mvn clean install -DskipTests'
                        }
                    }
                }

                stage('Build Notification Service') {
                    steps {
                        dir('notification-service') {
                            sh 'mvn clean install -DskipTests'
                        }
                    }
                }

                stage('Build File Storage Service') {
                    steps {
                        dir('file-storage') {
                            sh 'mvn clean install -DskipTests'
                        }
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
