pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/GURitch/demoTomcatJenkins.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                sshagent(credentials: ['Jenkins SSH Key']) {
                    sh 'scp target/dist/DemoApplication.war guritch@172.26.129.25:/opt/tomcat/webapps'
                }
            }
        }
    }
}
