node {
   def mvnHome
  stage('Prepare') {
      git url: 'https://github.com/kesavkummari/javacodescan.git', branch: 'main'
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
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore test"
  }
  stage ('Package') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore package -D"
  }
  stage ('Verify') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore verify -D"
  }
  stage ('Install') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore install -D"
  }
  stage ('Deliver & Deployment') {
      sh 'curl -u admin:redhat@123 -T target/**.war "http://54.221.91.226:8080/manager/text/deploy?path=/kesav&update=true"'
  }
  stage ('SmokeTest') {
      sh 'curl --retry-delay 10 --retry 5 "http://3.87.125.112:8080/kesav"'
  }
}
