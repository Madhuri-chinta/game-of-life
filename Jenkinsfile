pipeline {
    agent { label 'UBUNTU_NODE1'}
    // triggers { cron ('*/2 * * * 6') }
    triggers { pollSCM ('*/2 * * * 6') }
    parameters { string(name: 'MVN_GOAL', defaultValue: 'package', description: 'maven package') }
    stages {
        stage ('vcs') {
            steps {
                git url: 'https://github.com/wakaleo/game-of-life.git ',
                    branch: 'master'
                }
        }
        stage ('build') {    
            steps {
                sh export "PATH=/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH"
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
   
     
              
      
    
  
