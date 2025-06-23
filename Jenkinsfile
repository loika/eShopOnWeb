pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('test') {
      parallel {
        stage('unit') {
          steps {
            sh 'dotnet test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('fonctionnel') {
          steps {
            warnError(message: 'probleme') {
              sh 'dotnet test tests/FunctionalTests'
            }

          }
        }

      }
    }

    stage('deploy') {
      steps {
        sh 'dotnet publish eShopOnWeb.sln -o /var/aspnet'
        dir(path: '/var/aspnet') {
          archiveArtifacts(artifacts: '*', onlyIfSuccessful: true)
        }

      }
    }

  }
}