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
          triggeredBy user
        }
      }
      steps {
        script {
          echo 'condition met'
          echo 'Pulled - ' + env.GIT_BRANCH
        }
      }
    }
  }
}
