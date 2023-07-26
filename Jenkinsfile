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
        //stage ('Sonarqube Analysis') {
            //steps {
                //withSonarQubeEnv('SONAR_CLOUD') {
                //  sh 'mvn clean package sonar:sonar -Dsonar.projectKey="Jenkins123" -Dsonar.projectName="Jenkins"'
          //  }
       // }
       // } 
       // Game of life application run with java-8.Sonarqube did not support below Java-11 versions,only support 
       //from Java-11 to higher versions
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
    post {
        failure {
           mail subject : "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is failure",
                body : "Use this URL ${BUILD_URL} for more info",
                from : "${GIT_COMMITTER_EMAIL}", // here pass jenkins environmental variable 
                to : "${GIT_AUTHOR_EMAIL}" // here also pass jenkins environmental variable 
        }
        success {
            mail subject : "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is success",
                 body : "Use this URL ${BUILD_URL} for more info",
                 from : 'madhu123@gmail.com',
                 to : 'sweety123@gmail.com'
        }
    }      
      }
   
     
              
      
    
  
