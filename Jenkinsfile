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
         when {
        branch 'master'
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
       when {
        branch 'master'
    }

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

    stage('DockerBnP') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'gowthamihv') {
            def dockerImage = docker.build("gowthamihv/sysfoo:v${env.BUILD_ID}", "./")
            dockerImage.push()
            dockerImage.push("latest")
            dockerImage.push("dev")
          }
        }

      }
    }
   stage('Deploy to Dev') {
      when {
             beforeAgent true
             branch  'master'
           }

      agent any

      steps {
        echo 'Deploying to Dev Environment with Docker Compose'
        sh 'docker-compose up -d'
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
