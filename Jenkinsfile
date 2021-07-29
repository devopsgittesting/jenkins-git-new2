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
            steps {
                    sh 'mvn package -Dv=${BUILD_NUMBER}'
                }
            }
        stage('Success') {
           when {
       
               expression { currentBuild.result == 'SUCCESS' }
       
      }
      steps {
        echo "hello"
      }
    
            
         
        steps {
             
           archiveArtifacts '**/target/*.war'
             }     
        }
    }
       
}
