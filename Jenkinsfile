pipeline {
    agent any
    tools{
        maven 'maven_3_9_8'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/VigneshbabuOfficial/docker-compose-spring-boot-postgres-jenkins-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u vigneshofficial2020 -p ${dockerhubpwd}'

}
                   sh 'docker push vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation'
                }
            }
        }
       
    }
}
