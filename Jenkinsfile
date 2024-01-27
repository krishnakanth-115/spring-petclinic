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
          stage('sonar analysis') {
            steps {
                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('SONAR_CLOUD') {
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=springpetclinic1'
                }
            }
     }
       stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/spring-petclinic-*.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
     } 
}
