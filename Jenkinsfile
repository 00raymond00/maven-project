pipeline {
    agent any

    tools {
        maven 'localMaven'
        org.jenkinsci.plugins.docker.commons.tools.DockerTool 'localDocker'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
                sh "docker build -t tomcatwebapp:${env.BUILD_ID} ."
            }    
        }
    }
}