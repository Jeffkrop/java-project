properties([pipelineTriggers([githubPush()])])
  node('linux') {
    stage('Unit Tests') {
      git 'https://github.com/jeffkrop/java-project.git'
      sh "env"
      sh 'ant -f test.xml -v'
      junit 'reports/result.xml'
    }
    stage('Build') {
      sh 'ant -f build.xml -v'
    }
    stage('Report') {
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '83429242-4015-4c8c-9340-530967d54c1e', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    // some block
         aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins
        }  
    }
}
