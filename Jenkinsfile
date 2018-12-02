node('linux') {
    stage('Unit Tests') {
      sh 'ant -f test.xml -v'
      junit 'reports/result.xml'
    }
    stage('Build') {
      sh 'ant -f build.xml -v'
    }
    stage('Deploy'){
   s3Upload consoleLogLevel: 'INFO', dontWaitForConcurrentBuildCompletion: false,
       entries: [[bucket: 'homework-11/rectangle-${BUILD_NUMBER}.jar', 
       excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, 
       managedArtifacts: false, noUploadOnFailure: true, selectedRegion: 'us-east-1', 
       showDirectlyInBrowser: false, sourceFile: '*', storageClass: 'STANDARD', 
       uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', 
       profileName: '', userMetadata: []}
    stage('Report') {
    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 
                      'AWS_ACCESS_KEY_ID', credentialsId: 'a27f19d8-aafb-4dd1-8819-048f66e5e14c', 
                      secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
       sh 'aws cloudformation describe-stack-resources --stack-name Jenkins --region us-east-1' 
    }
  }     
}
