pipeline{
    agent any
    tools{
        maven 'maven_3_8_6'
    }
    stages{
        stage('build maven project'){
             steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jeffdumelod/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('build docker image'){
            steps{
                script{
                    sh 'docker build -t jeffdumelod/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u jeffdumelod -p ${dockerhubpwd}'
}
                   sh 'docker push jeffdumelod/devops-integration'
                }
            }
        }
       
    }
}