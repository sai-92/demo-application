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
        sh 'aws s3 cp webapp/target/webapp.jar s3://demokrishnas3us'
      }
    }
//     stage('Deploy to tomcat') {
//       steps {
//         sshagent(['tomcat-server-details']) {
//         sh 'scp -o "StrictHostKeyChecking=no" webapp/target/webapp.war ubuntu@54.219.35.228:/opt/tomcat/webapps'
//         }
//       }
//     }
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