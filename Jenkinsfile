pipeline{
        agent {
                docker {
                image 'maven'
                // args '-v $HOME/.m2:/root/.m2'
                args '-u root'
                }
        }
        stages{
              stage('Quality Gate Statuc Check'){
                  steps{
                      script{
                      withSonarQubeEnv('sonarserver') { 
                      sh "mvn sonar:sonar"
                       }
                    //   timeout(time: 1, unit: 'HOURS') {
                    //   def qg = waitForQualityGate()
                    //   if (qg.status != 'OK') {
                    //        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                    //   }
                    // }
		    sh "mvn clean install"
                  }
                }  
              }
            stage("deploy"){
            steps{
              sshagent(['Ubuntu']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ubuntu@3.84.22.129:/opt/tomcat/webapps"
                    }
                }
            }
        }
}