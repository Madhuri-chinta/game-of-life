pipeline {
    agent none
    stages {
        stage('vcs') {
            steps {
                git branch : 'master',
                    url: 'https://github.com/jenkinsci/platformlabeler-plugin.git'    
            }
        }
        
    }
}