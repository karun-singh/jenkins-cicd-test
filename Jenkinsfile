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
    stage('Test curl') {
      steps{
        script{
          sh '''response_code=$(curl -s -o /dev/null -w \'%{http_code}\\n\' --connect-timeout 5 --retry 5 --retry-connrefused -XGET https://api-docker.catalogue.iudx.io/api)

          if [[ "$response_code" -ne "200" ]]
          then
            echo "Health check failed"
            exit 1
          else
            echo "Health check complete; Server is up."
            exit 0
          fi
          ''' 
        }
      }
    }
  }
}
