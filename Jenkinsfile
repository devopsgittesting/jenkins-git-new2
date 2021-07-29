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
        
            
          stage ('Archive Stage') {
            steps {
             
                archiveArtifacts '**/target/*.war'
                }
            }   
             stage ('Deploy on Webserver Stage') {
            steps {
             
                   sh "sudo cp -rf /var/lib/jenkins/workspace/jenkins-tag-pipeline/target/*.war /root/jenkins/apache-tomcat-9.0.48/webapps"
           
              }
            }   
    }
    
    post {
    success {
   stage ('Archive Stage') {
            steps {
             
                archiveArtifacts '**/target/*_success.war'
                }
            }   
        
    }
    }      
}
