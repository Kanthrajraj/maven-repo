pipeline {
    // Add your slave label name
    agent { label 'slave_jenkins' }
    tools {
        maven 'maven-test'
    }
    stages {
        stage ('Checkout_SCM') {
            steps {
                checkout scm
            }
        }

        stage ('Maven_Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage ('Deploy_Tomcat') {
            steps {
                sshagent(['Tomcat']) {
                    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.116.183:/opt/tomcat9/webapps"
                }
            }
        }
    }
}
