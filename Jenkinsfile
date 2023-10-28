pipeline {
    agent any
    tools {
        maven "Maven3"
    }
    stages {
        stage ("Initialize") {
            steps{
                sh '''
                    
                    echo "PATH = ${PATH}"
                    echo "M3_HOME = ${PATH}"

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
                    // new update check
                    // sh '''
                    //     // sudo chmod -R 755 /root/prod/apache-tomcat-9.0.82/webapps
                    //     // sudo chown -R ubuntu:ubuntu /root/prod/apache-tomcat-9.0.82/webapps
                    //     sudo setfacl -m g:ubuntu:rwx -R /root/
                    // '''
                    
                    
                    sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@54.237.225.107:/home/ubuntu/prod/apache-tomcat-9.0.82/webapps/webapp.war'
                }
            }
        }
    }
}