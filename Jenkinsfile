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
      aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins
    }
}
