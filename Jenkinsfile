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
                scannerHome = tool 'SonarScanner'
            }
            steps {
                withSonarQubeEnv('SonarServer') {
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.sonar.login=4d6d1f8fd9e42c36736574e77e5a0f4a8cfe1146"
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