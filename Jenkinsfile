pipeline {
    agent any
    tools{
        jdk  'jdk11'
        maven  'maven3'

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/taimoor30/jenkins-pipeline-example/.git'
            }
        }
        
        stage('COMPILE') {
            steps {
                sh "mvn clean compile -DskipTests=true"
            }
        }
        
        stage('OWASP Scan') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ ', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests=true"
            }
        }
    }
}
