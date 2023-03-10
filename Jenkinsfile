pipeline {
    agent any
    stages {
        stage('vcs') {
            steps {
                git branch : 'master',
                    url: 'https://github.com/Madhuri-chinta/game-of-life.git'    
            }
        }
        stage('package') {
            steps {
                sh """export PATH=/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH
                             mvn package sonar:sonar"""
                }
            }   
        }
    }
}
