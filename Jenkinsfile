properties([pipelineTriggers([githubPush()])])
  node('linux') {
    stage('Unit Tests') {
      env | sort
      git 'https://github.com/jeffkrop/java-project.git'
      sh 'ant -buildfile test.xml'
      sh 'ant -f test.xml -v'
      junit 'reports/result.xml'
    }
    stage('Build') {
      sh 'ant'
    }
    stage('Results') {
      junit 'reports/*.xml'
    }
}
