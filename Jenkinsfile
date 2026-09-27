// def appVersion = ""

pipeline {
    agent {
        node {
            label 'ROBOSHOP'
        }
    }

    environment {
        def appVersion = ""
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 15, unit: 'MINUTES')
    }

    stages {
        stage('Read version') {
            steps {
                script {
                    // Requires "Pipeline Utility Steps" plugin
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version

                    echo "The application version is: ${appVersion}"
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh """
                        echo "Checking app version: ${appVersion}"
                        echo "Building"
                    """
                }
            }
        }

        stage('Install dependencies') {
            steps {
                script {
                    sh """
                        echo "Installing the dependencies"
                        npm install
                        echo "Installed
                         the dependencies"

                        npm audit fix --force
                        echo " npm audit issues fixed "
                    """
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh """
                        echo "Testing version: ${appVersion}"
                    """
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh """
                        echo "Deploying version: ${appVersion}"
                    """
                }
            }
        }
    }

    post {
        always {
            echo 'I will always say Hello again!'
        }

        success {
            echo 'I will run when success'
        }

        failure {
            echo 'I will run when it is failed'
        }
    }
}