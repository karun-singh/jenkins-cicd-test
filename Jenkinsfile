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
        allOf{
          anyOf {
            changeset "sampleFile.yaml"
            changeset "testFile.txt"
            triggeredBy cause: 'UserIdCause'
          }
          expression {
            return env.GIT_BRANCH == 'origin/master';
          }
        }
      }
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
