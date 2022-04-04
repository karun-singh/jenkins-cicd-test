pipeline {

  environment {
    registryCredential = 'karun-ghcr'
    GIT_HASH = GIT_COMMIT.take(7)
  }

  agent { 
    node {
      label 'slave1' 
    }
  }

  stages {
    stage('Test conditional') {
      steps {
        script {
          echo 'Pulled - ' + env.GIT_BRANCH
          if (env.BRANCH_NAME == 'origin/master') {
            echo 'I only execute on the master branch'
          } 
          else if (env.BRANCH_NAME == 'origin/v3.5.0'){
            echo 'I execute on v3.5.0 branch'
          }
          else{
            echo 'did not meet any conditions'
          }
        }
      }
    }
  }
}