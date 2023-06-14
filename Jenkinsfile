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
                        echo "jenkins ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
                        sudo scp -o StrictHostKeyChecking=no target/*.war ubuntu@23.23.255.135:prod/apache-tomcat-9.0.76/webapps/webapp.war
                    '''
                }
            }
        }
    }
}