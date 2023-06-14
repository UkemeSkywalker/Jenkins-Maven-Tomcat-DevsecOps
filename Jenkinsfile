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
                script {
                        def file_path = '/var/lib/jenkins/workspace/Webapp-ci-cd-project/target'
                        sshagent(['tomcat']) {
                            sh 'scp -o StrictHostKeyChecking=no ${file_path}/WebApp.war ubuntu@23.23.255.135:prod/apache-tomcat-9.0.76/webapps/webapp.war'
                        }
                }
            }
        }
    }
}