node('linux') {
    stage('Unit Tests') {
      git 'https://github.com/jeffkrop/java-project.git'
      sh 'ant -f test.xml -v'
      junit 'reports/result.xml'
    }
    stage('Build') {
      sh 'ant -f build.xml -v'
    }
    stage('Results') {
    junit 'reports/*.xml'
    }
    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'a27f19d8-aafb-4dd1-8819-048f66e5e14c', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    // some block
        aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins
    }
}
