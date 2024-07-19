pipeline {
    agent any
    tools{
        maven 'maven_3_9_8'
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
                        bat 'docker build -t vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation .'
                    } else {
                        sh 'docker build -t vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation .'
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
						withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
							bat 'docker login -u vigneshofficial2020 -p ${dockerhubpwd}'
						}
					bat 'docker push vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation'
				   
                    } else {
						withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
							sh 'docker login -u vigneshofficial2020 -p ${dockerhubpwd}'
						}
                   sh 'docker push vigneshofficial2020/docker-compose-spring-boot-postgres-jenkins-automation'
                    }
                }
            }
        }
       
    }
}
