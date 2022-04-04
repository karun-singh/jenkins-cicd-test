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
    hen{
        anyof{
          expression {
            return env.GIT_BRANCH == 'origin/master';
          }
          expression {
            return env.GIT_BRANCH == 'origin/v3.5.0';
          }
        }
      }
    stage('Test conditional') {
      steps {
        script {
          echo 'Pulled - ' + env.GIT_BRANCH
          if (env.GIT_BRANCH == 'origin/master') {
            echo 'I only execute on the master branch'
          } 
          else if (env.GIT_BRANCH == 'origin/v3.5.0'){
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