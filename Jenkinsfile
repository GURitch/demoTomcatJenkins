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
                            deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', url: 'http://tomcat.example.com:8085/')], contextPath: 'myapp', war: '**/*.war'
                        }
        }
    }
}
