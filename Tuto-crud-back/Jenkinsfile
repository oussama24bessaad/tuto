pipeline {
      environment {
          dockerimagename = "mehdijebali/crud-back"
          dockerImage = ""
      }
      agent any
      tools {maven "LocalMaven"}      
            
      stages {
            
            stage('Initialization') {
                  steps {
                        echo '**** Starting Pipeline Job ****'
                  }
            }
            stage('Code Quality Check via SonarQube') {
                  steps {
                        script {
                        def scannerHome = tool 'sonarqube';
                              withSonarQubeEnv("sonarqube") {
                              sh "${tool("sonarqube")}/bin/sonar-scanner \
                              -Dsonar.projectKey=Backend \
                              -Dsonar.sources=src \
                              -Dsonar.java.binaries=target \
                              -Dsonar.host.url=http://localhost:9000"
                              }
                        }                  
                  }
            }                  
            stage('Build Jar File') {
                  steps {
                        echo '**** Build jar file ****'
                        sh 'mvn clean package'
                  }
            }
            stage('Release Docker Image') {
                  environment {
                        registryCredential = 'dockerhub'
                  }
                  steps {
                        echo '**** Build Docker Image ****'
                        script{
                              dockerImage = docker.build dockerimagename
                              docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) 
                              {dockerImage.push("latest")}
                        }
                  }
            }
            stage('Deploy to k8s') {
                  steps {
                        echo '**** Deploy Application ****'
                        withCredentials([ string(credentialsId: 'k8s', variable: 'api_token') ]) { sh 'kubectl --token $api_token --server https://192.168.49.2:8443/ --insecure-skip-tls-verify=true apply -f ./K8s '}
                  }
            }          
      }      
}