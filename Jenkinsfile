pipeline {
    agent any
    tools {
        maven 'Maven 3.x' // Make sure this matches the Maven installation in Jenkins
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Development Server') {
            steps {
                script {
                    def warFile = "target/devops.war" // Adjust according to your project structure
                    def tomcatServer = "http://localhost:8080/manager/text"
                    def credentialsId = 'tomcat-credentials' // Jenkins credentials ID

                    withCredentials([usernamePassword(credentialsId: credentialsId, passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                        sh "curl -u ${USERNAME}:${PASSWORD} --upload-file ${warFile} ${tomcatServer}/deploy?path=/devops-development&update=true"
                    }
                }
            }
        }
    }
}
