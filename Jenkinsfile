pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=Petclinic \\
  -Dsonar.host.url=http://54.90.174.3:9000 \\
  -Dsonar.login=sqp_4f2df15440bf8c8fd39fa3e531df037d74e6dc89'''
      }
    }

  }
}