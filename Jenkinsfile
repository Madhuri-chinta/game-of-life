pipeline {
    agent { label 'UBUNTU_NODE1'}
    triggers { cron ('*/2 17 * * 6') }
    stages {
        stage ('vcs') {
            steps {
                git url: 'https://github.com/wakaleo/game-of-life.git ',
                    branch: 'master'
                }
        }
        stage ('build') {    
            steps {
                sh 'export "PATH=/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH" && mvn package'
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
   
     
              
      
    
  
