node {
   def mvnHome
  stage('Prepare') {
      git url: 'https://github.com/uday898989/sonar-code-jenkins-project.git', branch: 'main'
      mvnHome = tool 'maven'
   }
  stage ('Code Quality') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore sonar:sonar"
  }

  stage ('Clean') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean"
  }
  stage ('Validate') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore validate"
  }
  stage ('Compile') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore compile"
  }
  stage ('Test') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore test -DskipTests"
  }
  stage ('Package') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore package -DskipTests"
  }
  stage ('Verify') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore verify -DskipTests"
  }
  stage ('Install') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore install"
  }
  stage ('Deliver & Deployment') {
      sh 'curl -u admin:redhat@123 -T target/**.war "http://3.110.143.221:8080/manager/text/deploy?path=/malli&update=true"'
  }
  stage ('SmokeTest') {
      sh 'curl --retry-delay 10 --retry 5 "http://3.110.143.221:8080/malli"'
  }
}
