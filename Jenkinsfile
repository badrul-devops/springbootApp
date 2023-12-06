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
                script{
                withSonarQubeEnv(credentialsId: 'sonar-jenkins') {
    
                    sh 'mvn sonar:sonar'
                }
            }
            }
        }
        stage("docker build"){
            steps{
                sh "docker build -t springbootapp ."
            }
        }
        stage("docker push"){
            steps{
                script{
                echo "pushing the image to dockerhub"
                withCredentials([usernamePassword(credentialsId: "dockerHub",passwordVariable: "dockerHubPass" ,usernameVariable: "dockerHubUser" )]){
                sh "docker tag springbootapp ${env.dockerHubUser}/springbootapp:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}" 
                sh "docker push  ${env.dockerHubUser}/springbootapp:latest"
        }
        }
        }


    }

    }
}