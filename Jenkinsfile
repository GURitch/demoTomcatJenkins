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
            when {
                branch 'master'
            }
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'Jenkins SSH Key', keyFileVariable: 'KEY_FILE')]) {
                    sh '''
                        scp -i $KEY_FILE target/demo-0.0.1-SNAPSHOT.war guritch@172.26.129.25:/opt/tomcat/webapps
                    '''
                }
            }
        }
    }
}
