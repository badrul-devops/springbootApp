pipeline{
    agent any
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
    }
}