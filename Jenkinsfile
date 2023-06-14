pipeline {
    agent any
    tools {
        maven "Maven"
    }
    stages {
        stage ("Initialize") {
            steps{
                sh '''
                    
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${PATH}"

                '''
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage ('Deploy-to-Tomcat') {
            steps{
                sshagent(['tomcat']) {
                    // // new update check
                    sh '''
                        ls
                        pwd
                    '''
                }
            }
        }
    }
}