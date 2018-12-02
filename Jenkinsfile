node('linux') {
    stage('Unit Tests') {
      git 'https://github.com/jeffkrop/java-project.git'
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
