pipeline {
      agent any
   tools {
       maven "maven"
       jdk "java"
   }
    stages {
        stage("git clone"){
            steps{
                git 'https://github.com/yadhu870/jenkins-test.git'
            }
        }
            stage("maven build"){
                steps{
                    sh "mvn clean install"
                }
            }
            stage("nexus-repo"){
                steps{
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'webapp',
                            classifier: '',
                            file: 'target/webapp.war',
                            type: 'war'
                            ]
                            ],
                            credentialsId: 'nexus',
                            groupId: 'com.app.raghu',
                            nexusUrl: '52.42.159.17:8080',
                            nexusVersion: 'nexus3',
                            protocol: 'http',
                            repository: 'yadhu-relese',
                            version: '${BUILD_NUMBER}'
            }
        }
         stage("deploy to tomcat"){
     steps{
         sshagent(['a4a074d6-0481-4476-a01a-1b36f1829f1e']) {
     sh 'scp -o StrictHostKeyChecking=no target/webapp.war root@35.164.91.60:/opt/tomcat/webapps/'
}
     }
 }

        }
    }