pipeline{
    agent any
    tools{
        jdk 'java'
        maven 'maven'
    }
    stages{
        stage("git checkout"){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/badrul-devops/springbootApp.git']])
            }
        }
        stage("build"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("sonarscan"){
            steps{
                withSonarQubeEnv(credentialsId: 'sonar-jenkins') {
    
                    sh 'mvn sonar:sonar'
                }
            }
        }

    }
}