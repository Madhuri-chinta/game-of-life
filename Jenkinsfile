pipeline {
    agent { label 'UBUNTU_NODE1'}
    // triggers { cron ('*/2 * * * 6') } with cron
    // triggers { pollSCM ('*/2 * * * 6') } with pollSCM
    // parameters { string(name: 'MVN_GOAL', defaultValue: 'package', description: 'maven package') } with only one option
    parameters { choice(name: 'MVN_GOAL', choices: ['package', 'install', 'clean package', 'clean test'], description: 'maven') }
    stages {
        stage ('vcs') {
            steps {
                git url: 'https://github.com/wakaleo/game-of-life.git ',
                    branch: 'master'
                }
        }
        stage ('build') { 
            tools {
                jdk 'JDK_8'
            }   
            steps {
                // sh 'export "PATH=/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH"' (no tool configuration)
                sh "mvn ${params.MVN_GOAL}"
            }

            }
        stage ('archiveArtifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war', 
                                 onlyIfSuccessful: true,
                                 allowEmptyArchive : false
            }
        }
        stage ('testresults') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml',
                      allowEmptyResults: true
  
            }              
            }
        }   
      }
   
     
              
      
    
  
