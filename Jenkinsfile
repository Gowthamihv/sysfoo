pipeline {
  agent none
  stages {
   
    stage('build') {
       when {
        branch 'master'
    }

      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'compiling'
        sh 'mvn compile'
      }
    }

    stage('test') {
       when {
        branch 'master'
    }

      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'run unittest'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      

      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'generatinga artifcat'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

  }
  tools {
    maven 'Maven 3.6.1'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}
