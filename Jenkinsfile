pipeline {
    agent {
  label 'java'
    }
    stages{
        stage('get code') {
            steps{
                git branch: 'main', url: 'https://github.com/ganeshmerwade/Java-project-2.git'
            }
        }

        
        stage('build') {
            steps{
                sh '''
                    mvn clean install
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
}
}