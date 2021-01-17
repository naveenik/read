pipeline {
    agent any
    environment {
        PATH = "/opt/apache-maven-3.6.3/bin:$PATH"
    }
    stages {
        stage("Git pull new"){
            steps{
               git branch: 'master', credentialsId: 'git-cred-navin-latest', url: 'https://github.com/naveenik/read.git'
            }
        }
        stage("build code"){
            steps{
              sh "mvn clean install"
            }
        }
        stage("deploy"){
            steps{
              sshagent(['deploy_uesr']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@13.234.32.208/opt/tomcat/webapps"
                }
            }
        }
    }
}
