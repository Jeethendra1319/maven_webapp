pipeline{
    agent any
    environment {
        PATH = "$PATH:/usr/share/maven/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/nimbuswiztech/maven_webapp.git'
            }
         }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }

        stage('Run unit test') {
            steps {
                sh 'mvn test'
            }
        }
       stage('deploy'){
            steps{
                sshagent(['Tomcat-demo']) {
                    sh "scp -o StrictHostKeyChecking=no target/demo.war ubuntu@54.90.214.50:/var/lib/tomcat9/webapps"

                }
            }
        }
       
    }
}
