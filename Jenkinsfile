pipeline{
   agent any
tools{
     maven 'Maven'
}

 
   stages {

              stage("Code Checkout") {
                                steps {
                                       git url: 'https://github.com/vinitgarg/world.git'
                                      }
                                     }
              stage('Build Stage') {
                               steps{
                                        bat 'mvn package'
                                     }
                                    }
              stage('Compile Stage'){
                                steps{
                                       bat 'mvn clean compile'
                                      }
                                     }
              stage('Testing Stage'){
                                steps{
                                      bat 'mvn test'
                                     } 
                                    }
              stage('build && SonarQube analysis'){
                                steps {
                                       withSonarQubeEnv('Sonarqube') {
                                                                     bat 'mvn sonar:sonar -Dsonar.projectKey=Pipeline_1 -Dsonar.host.url=http://localhost:9000 -Dsonar.login=276c279e5495d759328a6798528deb8d3b411b2d'
                                                                 } 
                                      } 
                                    }
              stage('Deploy artifact'){
                                steps{
                                      rtServer (id: 'Artifactory',url: 'http://localhost:8081/artifactory',username: 'admin',password: 'password')
                                      rtUpload (serverId: 'Artifactory',spec: '''{"files": [{ "pattern": "/**.war","target": "maven_artifact/"}]}''')
                                      }
                                     }
                                     
                  stage('Deploy to tomcat'){
                                steps{
                                       bat "copy target\\firstmvn.war \'C:\\Users\\vinitgarg\\apache-tomcat-8.5.51\\webapps'"
                                     }
                                   }
             
                                 }
}
