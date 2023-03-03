pipeline {
    agent {
  label 'java'
    }
    parameters {
  choice choices: ['main', 'dev', 'staging', 'feature'], description: 'select branch', name: 'branch'
}
    stages{
        stage('get code') {
            steps{
                git branch: "${params.branch}", credentialsId: 'github', url: 'https://github.com/ganeshmerwade/javawbapp_withtest.git'
            }
        }

        
        stage('build') {
            steps{
                sh '''
                    mvn -B -DskipTests clean install
                '''
            }
        }
        stage("build & SonarQube analysis") {
            steps {
              withSonarQubeEnv('sonaqube-8.9.9') {
                sh 'mvn sonar:sonar'
              }
            }  
}
        stage('test') {
            steps{
                sh '''
                    mvn test
                '''
            }
        }       
        stage('deploy') {
            steps{
                sh '''
                    scp -v -o StrictHostKeyChecking=no *.war ubuntu@172.31.12.87:/var/lib/tomcat9/webapps
                '''
            }
        }
}
}