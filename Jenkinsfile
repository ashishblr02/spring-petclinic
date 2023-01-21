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
        sh '''./mvnw verify sonar:sonar \\
  -Dsonar.host.url=http://localhost:9000/ \\
  -Dsonar.projectKey=Petclinic \\  
  -Dsonar.login=sqp_75bf4af384857db4b80b737008624a1ab08fd6fd'''
      }
    }

  }
}