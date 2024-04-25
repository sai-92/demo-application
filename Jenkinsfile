pipeline {
  agent any
  tools {
    maven 'maven'
  }
   triggers {
    pollSCM '* * * * *'
  }
  stages {
    stage('Build app') {
      steps {
        sh 'mvn clean install package'
      }
    }
    stage('Push Artifact to S3') {
      steps {
       sh 'aws s3 cp /var/lib/jenkins/workspace/maven_job/target/demo-application-0.0.1-SNAPSHOT.jar s3://demokrishnas3us'
      }
    }
    stage('Deploy to tomcat') {
      steps {
        sshagent(['tomcat-server-details']) {
        sh 'scp -o "StrictHostKeyChecking=no" /var/lib/jenkins/workspace/maven_job/target/demo-application-0.0.1-SNAPSHOT.jar ubuntu@54.153.63.193:/opt/tomcat/webapps'
        }
      }
    }
    // stage('Deploy to tomcat') {
    //   steps {
    //        sh 'sudo scp -i demo.pem -o "StrictHostKeyChecking=no" webapp/target/webapp.war ubuntu@65.0.3.198:/opt/tomcat/webapps'
    // }
    // }
}
// post {
//      always {
//        emailext to: 'lakshmiphanindrarudra@gmail.com',
//        attachLog: true, body: "Dear team pipeline is ${currentBuild.result} please check ${BUILD_URL} or PFA build log", compressLog: false,
//        subject: "Jenkins Build Notification: ${JOB_NAME}-Build# ${BUILD_NUMBER} ${currentBuild.result}"
//     }
// }
}