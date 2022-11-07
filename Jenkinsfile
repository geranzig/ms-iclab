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
 
        stage('Sonarqube') {
            environment {
                scannerHome = tool 'SonarServer'
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
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