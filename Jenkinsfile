pipeline {
    agent any
    stages {
        stage('vcs') {
            steps {
                git branch : 'master',
                    url: 'https://github.com/Madhuri-chinta/game-of-life.git'    
            }
        }
        stage('sonarqube') {
            steps {
                withSonarQubeEnv('madhuri') {
                    sh """export PATH=/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH
                             mvn clean package sonar:sonar"""
                }
            }   
        }
    }
}
