
Ошибка указывает на то, что метод sshagent не найден среди шагов (steps) вашего Jenkins Pipeline. Это связано с тем, что вы используете неправильный метод для выполнения SSH-команд.

Вместо sshagent вам нужно использовать withCredentials, чтобы передать учетные данные SSH в блок sh:

groovy
Copy code
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
