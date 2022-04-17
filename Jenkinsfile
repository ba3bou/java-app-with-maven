pipeline {
  agent any
  tools {
    maven 'Maven'
  }
  stages {
    stage('Initialize') {
      steps {
        sh '''
             echo "PATH = ${PATH}"
             echo "M2_HOME = ${M2_HOME}"
            '''
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage ('Deploy-To-Tomcat') {
      steps {
        sshagent(['tomcat']) {
          sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/webapp-test-pipeline-4/target/WebApp-test.war ubuntu@107.23.249.209:/prod/apache-tomcat-8.5.39/webapps/webapp.war'
        }      
      }
     } 
  }
}
