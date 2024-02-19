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
                            // Шаг для копирования WAR-файла на сервер Tomcat
                            deploy adapters: [tomcat8(credentialsId: 'tomcat-credentials', url: 'http://172.26.129.25:8080/')], contextPath: 'myapp', war: '**/*.war'
                        }
        }
    }
}
