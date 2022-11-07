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
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.sonar.login=3485ddcb5ff494defb182f6b0d5a826b2781321c"
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