pipeline {
    agent any
    tools {
        maven 'Maven3'  // Ensure Maven is installed
        jdk 'JDK21'     // Ensure JDK is installed
    }
    stages {
        stage('Checkout Code') {
            
            steps {
                git branch: 'main', url: 'https://github.com/yasminbx/diceroll'
               
            }
        
    
        }
        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('Run Unit Tests') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'  // Capture test reports
                }
            }
        }
        stage('Code Coverage Report') {
            steps {
                bat 'mvn jacoco:report'
            }
            post {
                always {
                    jacoco execPattern: 'target/jacoco.exec'
                }
            }
        }
    }
}
