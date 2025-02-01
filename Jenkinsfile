pipeline {
    agent any
    environment {
      MAVEN_OPTS="--add-opens java.base/java.lang=ALL-UNNAMED"   
    }    

    stages {   
        stage('Build with maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install'
            }
        }
        
             stage('Test') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        
            }
        stage('Code Qualty Scan') {

           steps {
                  withSonarQubeEnv('sonar-scanner') {
 

             sh "mvn -f SampleWebApp/pom.xml sonar:sonar"      
               }
            }
       }
        
                
        stage('deploy to tomcat') {
          steps {
            deploy adapters: [tomcat9(credentialsId: 'tomcatID', path: '', url: 'http://3.93.49.213:8080')], contextPath: 'webapp', war: '**/*.war'
          }

            
        }
            
        }
}
