node('linux') {
    stage('Unit Tests') {
      git 'https://github.com/jeffkrop/java-project.git'
      sh 'ant -f test.xml -v'
      junit 'reports/result.xml'
    }
    stage('Build') {
      sh 'ant -f build.xml -v'
    }
    stage('Deploy'){
        sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://homework-11'
    }
     stage('Report') {
     withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
                       credentialsId: '6b9c7ae5-4e91-4c2b-8d3f-f77e74d467f8', 
                       secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
       sh 'aws cloudformation describe-stack-resources --stack-name Jenkins --region us-east-1' 
    }
  }     
}
