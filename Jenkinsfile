pipeline {
  agent any
 

tools{

maven 'Maven 3.6.1'
}

 stages{
      stage("build"){
          steps{
              echo 'compiling'
              sh 'mvn compile'
          }
      }
      stage("test"){
          steps{
              echo 'run unittest'
              sh 'mvn clean test'
          }
      }
      stage("package"){
          steps{
              echo 'generatinga artifcat'
              sh 'mvn package -DskipTests'
          }
      }
  }

  post{
    always{
        echo 'This pipeline is completed..'
    }
  }
}

