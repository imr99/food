pipeline {
    agent any
    environment{
        PATH = "/usr/share/maven-3.0.5/bin:$PATH"
    }
    stages {
        stage('Git clone') {
            steps {
                git branch: 'master', url: "https://github.com/imr99/JavaCalculator.git"
            }
        }    
        stage('build code') {
            steps {
                sh ' mvn clean install'
            }
        }
        stage('build docker image') {
            steps {
                sh 'docker build -t imr99/calculator-app  .'
            }
        }
        stage("push docker image"){
            steps {
                script {
                    withCredentials([string(credentialsId: 'imr99', variable: 'dockerhubpwd')]) {
                    sh "docker login -u imr99 -p ${dockerhubpwd}"
}
                   sh "docker push imr99/calculator-app" 
                }
            }
        }
         
    }
}