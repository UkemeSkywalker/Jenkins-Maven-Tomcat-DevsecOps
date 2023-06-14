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
                    sh 'sudo -i'
                    sh 'echo pwd'
                    // sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@23.23.255.135:root/prod/apache-tomcat-9.0.76/webapps/webapp.war'

                }
            }
        }
    }
}