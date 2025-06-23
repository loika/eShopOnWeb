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
            sh 'dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('deploy') {
      steps {
        sh 'dotnet publish eShopOnWeb.sln -o /var/aspnet'
      }
    }

  }
}