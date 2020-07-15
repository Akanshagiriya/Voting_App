pipeline {
    agent any
        stages {
            stage("Building SONAR ...") {
               steps {
                   bat '''
                       cd Voting_App
                       mvn clean install
                       '''
                    }
                }

            stage('SonarQube') {
            steps{
                bat '''
                    mvn sonar:sonar \
                      -Dsonar.projectKey=VotingApp \
                      -Dsonar.host.url=http://localhost:9000 \
                      -Dsonar.login=dfd5ca3e624a63fbb5fc9d2d410c8eaf6f04605e
                '''
            } 
        }
            // Build The Project              
            stage('Build') {
                    tools {	
        			    jdk 'jdk1.8'
        			    maven 'apache-maven-3.6.3'
        	         }
                         steps {
                             git 'https://github.com/Akanshagiriya/Voting_App.git'
                           bat '''
                            java -version
            			    mvn -version
            			    mvn clean package
                            mvn clean install
                           '''
                         }
        }
       
  }      
}
