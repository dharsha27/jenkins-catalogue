// def appVersion = ""

pipeline {
    agent {
        node {
            label 'ROBOSHOP'
        }
    }

    environment {
        def appVersion = ""
        acc_id = "830067446715"
        project = "roboshop"
        component = "catalogue"
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

                        npm fund
                        echo " npm fund issues fixed "

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

        stage ('Docker build'){
            steps {
                script{
                    
                    echo "AWS ECR LOGIN "
                    withAWS (credentials: 'aws-creds' , region: 'us-east-1'){
                   sh """
                    
                    aws ecr get-login-password --region us-east-1 | docker login --username  AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazon.aws
                    echo "building the docker image"
                    docker build -t ${acc_id}.dkr.ecr.us-east-1.amazon.aws/${project}/${component}:${appVersion} .
                    echo "docker image build successfully "
                    echo "docker image pushing to the ecr "
                    docker push ${acc_id}.dkr.ecr.us-east-1.amazon.aws/${project}/${component}:${appVersion} 
                    echo "docker image push to ecr  successfully "
                    
                    """

                    }  
                        
                        echo "building the docker image"

                        
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