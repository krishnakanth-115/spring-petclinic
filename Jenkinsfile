pipeline{
     agent { label 'MAVEN' }
     triggers{ 
      pollSCM('* * * * *') 
      }
     stages{
        stage('scm'){
         steps{
             git branch: 'main',
            url: 'https://github.com/krishnakanthgoud/spring-petclinic.git'
         }
        }
     stage('build'){
           tools {
                 maven "3.9.5"
                }
           steps{
                sh "mvn package"
           }
       }
     
      stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
     } 


}
