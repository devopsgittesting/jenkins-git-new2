pipeline {
    agent any

    stages {
        stage ('BuildStage') {

            steps {
                fileExists 'pom.xml'
                
                    sh 'mvn compile install -Dv=${BUILD_NUMBER}'
               
                }
            }
        

        stage ('Testing Stage') {

            steps {
      
                    sh 'mvn clean test -Dv=${BUILD_NUMBER}'
                }
            }
        


        stage ('Deployment Stage') {
            
            when {
       
               expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                    sh 'mvn package install -Dv=${BUILD_NUMBER}'
              
                    archiveArtifacts '**/target/*.war'
             }     
        }
        
         when {
       
               expression { currentBuild.result == 'FAILURE' }
            }
            steps {
                    sh 'mvn package install -Dv=${BUILD_NUMBER}'
              
                    archiveArtifacts '**/target/*_failed.war'
             }     
        }
        
    }
       
}
