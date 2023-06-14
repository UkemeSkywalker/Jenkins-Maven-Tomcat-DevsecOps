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
                    // sh '''
                    //     sudo chmod -R 755 /root/prod/apache-tomcat-9.0.76/webapps
                    //     sudo chown -R ubuntu:ubuntu /root/prod/apache-tomcat-9.0.76/webapps
                    // '''
                    // sudo setfacl -m g:ubuntu:rwx -R /root/
                    
                    
                    sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@23.23.255.135:/root/prod/apache-tomcat-9.0.76/webapps/webapp.war'
                }
            }
        }
    }
}