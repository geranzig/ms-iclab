pipeline {
    agent any
    stages {
        stage('Compilación') {
            steps {
	     git branch: 'feature-estado-pais', url: 'https://github.com/geranzig/ms-iclab.git'
                sh './mvnw clean compile -e'
            }
        }
        stage('Test') {
            steps {
                sh './mvnw clean test -e'
            }
        }
        stage('Jar Code') {
            steps {
                sh './mvnw clean package -e'
            }
        }
        stage('Run Jar') {
            steps {
                sh 'nohup bash mvnw spring-boot:run &'
            }
        }
    }
}