currentBuild.displayName="Vprofile-v1--->"+currentBuild.number


pipeline{
    agent any
    stages{
        stage ("Git-Cloning"){
            
  // Blow stage for cloning data from Git-hub (using javademo Repository)   
            steps {
                git url: 'https://github.com/krishna1083/javademo.git'
            }
        }
  // Below stage for maven build
  
        stage ("Maven-Build"){
            steps {
                sh "mvn clean install"
            }
        }
      
 // Below stage for Uploading artifact (.war file) in to Nexus centrol repository
 
        stage ("Nexus-Artifact-uploader"){
           steps {
           nexusArtifactUploader artifacts: [[artifactId: 'vprofile-v1',
           classifier: '',
           file: 'target/vprofile-v1.war', type: 'war']],
           credentialsId: 'be2ded57-13b4-48e2-9fdd-8d5aa0e949b8',
           groupId: 'vprofile',
           nexusUrl: '52.91.161.84:8081//nexus/content/repositories/krishna/',
           nexusVersion: 'nexus2',
           protocol: 'http',
           repository: 'krishna',
           version: '$BUILD_ID'       
           }    
        }
   
   // Below stage for Tomcat-Deployment
  
        stage ("Tomcat-Deploy"){
            steps {
               sshagent(['deployer_userr']) {
  // some block
             sh "scp -o StrictHostKeyChecking=no target/vprofile-v1.war ubuntu@3.80.55.116:/opt/apache-tomcat-8.5.82/webapps"
} 
            }
        }
 
    }
}
