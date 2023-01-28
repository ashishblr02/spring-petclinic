pipeline {
  agent {
    node {
      label 'test'
    }

  }
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=Petclinic \\
  -Dsonar.host.url=http://10.10.0.22:9000 \\
  -Dsonar.login=sqp_8da06751f9d25cceeba4ca416347bc0338a2d565'''
      }
    }

    stage('Unit test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

    stage('Package') {
      steps {
        sh '''./mvnw package -DskipTests=true
'''
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh './mvnw spring-boot:run </dev/null &>/dev/null &'
          }
        }

        stage('integration and performance') {
          steps {
            sh './mvnw verify'
            junit '**/target/surefire-reports/*.xml'
            perfReport '**/target/jmeter/results/*'
          }
        }

      }
    }

  }
}