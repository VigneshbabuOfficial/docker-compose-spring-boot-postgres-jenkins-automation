pipeline {
    agent any
    tools{
        maven 'maven_3_9_8'
    }
	environment {
        DOCKERHUB_USERNAME = 'vigneshofficial2020@gmail.com'
        DOCKERHUB_PASSWORD = credentials('dockerhub-pwd')
    }
    stages{
        stage('SCM Checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/VigneshbabuOfficial/docker-compose-spring-boot-postgres-jenkins-automation']])
            }
        }
		stage('Build Maven'){
            steps{
				script{
					// Determine OS type
                    def isWindows = isUnix() ? false : true
                    if (isWindows) {
                        bat 'cd bezkoder-app & mvn clean install'
                    } else {
                        sh 'mvn clean install'
                    }
				}
            }
        }
        stage('Build docker image'){
            steps{
                script{
					// Determine OS type
                    def isWindows = isUnix() ? false : true
                    if (isWindows) {
                        bat 'cd bezkoder-app & docker build -t vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation .'
                    } else {
                        sh 'cd bezkoder-app & docker build -t vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation .'
                    }
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
					// Determine OS type
                    def isWindows = isUnix() ? false : true
                    if (isWindows) {
						withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'DOCKERHUB_PASSWORD')]) {
						
						bat 'echo %DOCKERHUB_PASSWORD% | docker login -u %DOCKERHUB_USERNAME% --password-stdin'
						}
					bat 'docker push vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation'
				   
                    } else {
						withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
							sh 'docker login -u vigneshofficial2020@gmail.com -p ${dockerhubpwd}'
						}
                   sh 'docker push vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation'
                    }
                }
            }
        }
       
    }
}
