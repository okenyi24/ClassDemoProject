pipeline {
    agent any
    tools {
        jdk 'myjava'
        maven 'mymaven'
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning..'
                // Use withCredentials to provide GitHub credentials
                withCredentials([usernamePassword(credentialsId: 'theitern', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        // Clone the private GitHub repository using the provided credentials
                        git 'https://github.com/theitern/DevOpsCodeDemo.git'
                    }
                }
            }
        }
        stage('Compile') {
            steps {
                echo 'Compiling..'
                sh 'mvn compile'
            }
        }
        stage('CodeReview') {
            steps {
                echo 'Code Review'
                sh 'mvn pmd:pmd'
            }
        }
        stage('UnitTest') {
            steps {
                echo 'Testing'
                sh 'mvn test'
            }
            post {
                success {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging..'
                sh 'mvn package'
            }
        }
    }
}
