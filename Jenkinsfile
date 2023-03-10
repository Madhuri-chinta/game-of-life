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
                sh 'export PATH="/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH"'
                }
        }
        stage('package') {
            steps {
                sh  'mvn package'
                }
        }
        stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "jfrog",
                    serverId: "madhuri",
                    releaseRepo: "libs-release-local",
                    snapshotRepo: "libs-snapshot-local"
                )
            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: "MAVEN_GOAL", // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "jfrog"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "madhuri"
                )
            }
        }   
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}

     
        