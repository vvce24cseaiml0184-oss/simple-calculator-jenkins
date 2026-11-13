
pipeline {
    agent any

    tools {
        jdk 'JDK 25'
        maven 'Maven-3.10'
    }

    stages {
        stage('SCM Synchronization') {
            steps {
                echo 'Pulling latest code changes from Git repository...'
                checkout scm
            }
        }

        stage('Static Verification') {
            steps {
                echo 'Checking Maven project layout rules...'
                bat 'mvn validate'
            }
        }

        stage('Compilation & Automated Testing') {
            steps {
                echo 'Compiling and running tests...'
                bat 'mvn clean package'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }
        failure {
            echo 'CI Pipeline failed and broken blah blah. Check console output.'
        }
    }
}
