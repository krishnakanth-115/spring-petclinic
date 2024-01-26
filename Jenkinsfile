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
                archiveArtifacts artifacts: '/home/ubuntu/workspace/workspace/mvn freestyle/target/spring-petclinic-3.2.0-SNAPSHOT.jar.original',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
     } 


}
