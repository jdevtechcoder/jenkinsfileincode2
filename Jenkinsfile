pipeline {
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jdevtechcoder/https://github.com/jdevtechcoder/jenkinsfileincode2']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t jtechcoder/jenkinsfileincode2 .'
                }
            }
        }
        stage('Push image'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerpipelinepwd', variable: 'dockerpipelinpwd')]) {
					sh 'docker login -u jtechcoder -p ${dockerpipelinpwd}'
					}
                   sh 'docker push jtechcoder/jenkinsfileincode2'
                }
            }
        }
        
    }
}