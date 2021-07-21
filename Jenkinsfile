pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'compiling'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'run unittest'
        sh 'mvn clean test'
      }
    }


    stage('package') {
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
