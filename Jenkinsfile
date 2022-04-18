pipeline {
      environment {
          dockerimagenamefront = "oussama24/crud-front"
          dockerImagefront = ""
          dockerimagenameback = "oussama24/crud-back"
          dockerImageback = ""
      }
      agent any
      tools {maven "LocalMaven"}      
            
      stages {
            
            stage('Initialization') {
                  steps {
                        echo '**** Starting Pipeline Job ****'
                  }
            }
            stage('Cloning Git') {
            steps {
                git 'https://github.com/oussama24bessaad/Tuto-crud-front'
                git 'https://github.com/oussama24bessaad/Tuto-crud-back'
            }
        }
//             stage('Code Quality Check via SonarQube') {
//                   steps {
//                         script {
//                         def scannerHome = tool 'SonarScanner';
//                               withSonarQubeEnv("sonarqube-server") {
//                               sh "${tool("SonarScanner")}/bin/sonar-scanner \
//                               -Dsonar.projectKey=tuto \
//                               -Dsonar.sources=src \
//                               -Dsonar.java.binaries=target \
//                               -Dsonar.host.url=http://localhost:9000"
//                               }
//                         }                  
//                   }
//             }                  
            stage('Build Jar File') {
                  steps {
                        echo '**** Build jar file ****'
                        sh 'mvn clean package'
                  }
            }
            stage('Release Docker Image Front') {
                  environment {
                        registryCredential = "dockerhub_credentials"
                  }
                  steps {
                        echo '**** Build Docker Image Front ****'
                        script{
                              dockerImagefront = docker.build dockerimagenamefront
                              docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) 
                              {dockerImagefront.push("latest")}
                        }
                  }
            }
             stage('Release Docker Image Back') {
                  environment {
                        registryCredential = "dockerhub_credentials"
                  }
                  steps {
                        echo '**** Build Docker Image Back ****'
                        script{
                              dockerImageback = docker.build dockerimagenameback
                              docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) 
                              {dockerImageback.push("latest")}
                        }
                  }
            }
//             stage('Deploy to k8s') {
//                   steps {
//                         echo '**** Deploy Application ****'
//                         withCredentials([ string(credentialsId: 'k8s', variable: 'api_token') ]) { sh 'kubectl --token $api_token --server https://192.168.49.2:8443/ --insecure-skip-tls-verify=true apply -f ./K8s '}
//                   }
//             }          
      }      
}
