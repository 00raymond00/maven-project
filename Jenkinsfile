pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: 'localhost', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'localhost', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "cp **/target/*.war ${params.tomcat_dev}:/Users/raymondho/_CODE_/tutorials/Jenkins/downloads/apache-tomcat-8.5.37-STAGING/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "cp **/target/*.war ${params.tomcat_prod}:/Users/raymondho/_CODE_/tutorials/Jenkins/downloads/apache-tomcat-8.5.37-PROD/webapps"
                    }
                }
            }
        }
    }
}