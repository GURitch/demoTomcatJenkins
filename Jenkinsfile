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
                withCredentials([usernamePassword(credentialsId: 'tomcat-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                           deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', url: 'http://192.168.1.108:8080/')], contextPath: 'webapps/myApp', war: '**/*.war'
               }
            }
        }
    }
}
