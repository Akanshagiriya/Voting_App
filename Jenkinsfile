pipeline {
    agent any
             options {
                    // Keep the 10 most recent builds
                buildDiscarder(logRotator(numToKeepStr:'10')) 
            }
        stages {
            stage('package'){
                steps{
                        bat '''
                            cd VotingApp
                             mvn clean package
                             mvn clean install
                             mvn -B verify
                            '''
                 }
            }
            // Build The Project              
            stage('Build') {
                         steps {
                             git 'https://github.com/Akanshagiriya/Voting_App.git'
                           bat '''
                             cd VotingApp
                            mvn clean install
                           '''
                         }
        }
          stage('SonarQube') {
            steps{
                bat '''
                     cd VotingApp
                    mvn sonar:sonar \
                      -Dsonar.projectKey=VotingApp \
                      -Dsonar.host.url=http://localhost:9000 \
                      -Dsonar.login=dfd5ca3e624a63fbb5fc9d2d410c8eaf6f04605e
                '''
            } 
        }
        stage('Build') { 
        	tools {	
        			jdk 'jdk 1.8'
        			maven 'apache-maven-3.6.3'
        	    }
    		steps {
    		    bat '''
    		        cd VotingApp
            		    java -version
            			mvn -version
            			mvn clean package
                	'''
    			}
    		}
    		
        
    	stage('Deploy') {
    		steps{
    			echo "Deploying"
    			        deploy adapters: [tomcat7(credentialsId: '21e30ec6-0d46-4ea8-9078-ef90a528a39f', path: '', url: 'http://localhost:8093')], contextPath: 'HappyTrip', war : '*/.war'
    			}

    }
  }      
}
