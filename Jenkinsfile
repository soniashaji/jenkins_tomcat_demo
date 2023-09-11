pipeline {
    agent any
    tools {
        maven 'maven-3.9'
    }
    parameters {
        string defaultValue: '100.26.235.195', name: 'tomcat-server'
    }
    stages{
        
        stage('checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/soniashaji/jenkins_tomcat_demo.git']])
            }    
        }
        stage('Build'){
            steps{
                echo 'Building Maven project'
                sh 'mvn clean install'
            }
        }
        stage('Deploy on Tomcat'){
            input {
                  message 'Ready To Deploy?'
                  ok 'OK'
            }
            steps{
                echo 'Deploying on Tomcat '
                sshagent(['tomcat-key']) {
                    sh 'scp -v -o StrictHostKeyChecking=no target/demowar-0.0.1-SNAPSHOT.war ubuntu@54.84.84.141:/opt/tomcat/webapps'
                }
            }
        }
        
    }
        

}
