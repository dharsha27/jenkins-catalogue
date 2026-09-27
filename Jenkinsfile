// pipeline {
//     agent { 
//         node { 
//             label 'ROBOSHOP' 
//         } 
//     }
//     //  environment {
//     //     COURSE = "Jenkins"
//     // }
//      options {
//         disableConcurrentBuilds()
//         timeout(time: 15, unit: 'MINUTES')
//     } 
//    /*  parameters {
//         string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
//         text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
//         booleanParam(name: 'DEPLOY', defaultValue: true, description: 'Toggle this value')
//         choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
//         password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
//     } */
//     // Build
//     stages {

//         stage('Read version'){
//             steps{
//                 script{
//                     def packageJson = readJSON file: 'package.json'
                    
//                     // Extract the version property
//                     def appVersion = packageJson.version
//                     echo " The application version is : ${appVersion}"
//                 }
//             }
//         }

//         stage('Build') {
//             steps {
//                 script {
//                     sh """
//                         echo "Building"
//                     //    /*  echo "Course is: ${COURSE}"
//                     //     echo "Hello ${params.PERSON}"
//                     //     echo "Biography: ${params.BIOGRAPHY}"
//                     //     echo "Toggle: ${params.TOGGLE}"
//                     //     echo "Choice: ${params.CHOICE}"
//                     //     echo "Password: ${params.PASSWOR */D}"
//                     """
//                 } 
//             }
//         }
//         stage('Test') {
//             steps {
//                 script {
//                     sh """
//                         echo "Testing"
//                     """
//                 }
//             }
//         }
//         stage('Deploy') {
//             // when {
//             //     // Evaluates the boolean parameter directly
//             //     expression { "${params.DEPLOY}" == "true" }
//             // }
//             /* input {
//                 message "Should we continue?"
//                 ok "Yes, we should."
//                 submitter "alice,bob"
//                 parameters {
//                     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
//                 }
//             } */
//             steps {
//                 script {
//                     sh """
//                         echo "Deploying"
//                     """
//                 }
//             }
//         }
//     }

//     post { 
//         always { 
//             echo 'I will always say Hello again!'
//         }
//         success { 
//             echo 'I will run when success'
//         }
//         failure { 
//             echo 'I will Run when it is failed'
//         }
//     }
// }

pipeline { 
    agent { 
        node any { 
            label 'ROBOSHOP' 
        } 

        environment {
                def appVersion = ""
        }
    } 
    
    options { 
        disableConcurrentBuilds() 
        timeout(time: 15, unit: 'MINUTES') 
    } 

      /*  parameters {
         string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
         text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
         booleanParam(name: 'DEPLOY', defaultValue: true, description: 'Toggle this value')
         choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
         password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
     } 
 */
    stages { 
        stage('Read version'){ 
            steps{ 
                script{ 
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
                        // echo "checking app version : ${appVersion}"
                        echo "Building"
                         
                    """ 
                } 
            } 
        } 
        
        stage('Test') { 
            steps { 
                script { 
                    sh """ 
                        echo "Testing" 
                    """ 
                } 
            } 
        } 
        
        stage('Deploy') { 
            steps { 
                script { 
                    sh """ 
                        echo "Deploying" 
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
            echo 'I will Run when it is failed' 
        } 
    } 
}
