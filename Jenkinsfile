pipeline {
    agent any

    tools {
        maven 'Maven3'    // Ensure Maven is installed
        jdk 'JDK21'       // Ensure JDK is installed
        git 'DefaultGit'  // Specify the Git tool installation
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/yasminbx/diceroll'
            }
        }

        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn clean package'  
                    } else {
                        bat 'mvn clean package' 
                    }
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn test'  
                    } else {
                        bat 'mvn test'  
                    }
                }
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }

        stage('Code Coverage Report') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn jacoco:report' 
                    } else {
                        bat 'mvn jacoco:report'  
                    }
                }
            }
            post {
                always {
                    jacoco execPattern: 'target/jacoco.exec'  
                }
            }
        }
    }
}
