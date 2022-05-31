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
      when {
        anyOf {
          changeset "sampleFile.yaml"
          changeset "testFile.txt"
          triggeredBy cause: 'UserIdCause'
        }
      }
      steps {
        script {
          echo 'condition met'
          echo 'Pulled - ' + env.GIT_BRANCH
        }
      }
    }
    stage{
      stages{
        stage('stage 1 nested'){
          steps{
            echo 'stage 1 executed'
          }
        }
        stage('stage 2 nested'){
          steps{
            echo 'stage 2 executed'
          }
        }
      }
    }
  }
}
