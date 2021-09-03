pipeline {
agent {
    node {
        label 'slave1'
    }
environment {
dotnet = 'path\\to\\dotnet.exe'
}
stages {
stage ('Checkout') {
            steps {
                 git credentialsId: 'userId', url: 'https://github.com/wonks2021/nettake1.git',branch: 'master'
            }
}
stage ('Restore PACKAGES') {     
         steps {
             sh "dotnet restore --configfile NuGet.Config"
          }
        }
stage('Clean') {
      steps {
            sh 'dotnet clean'
       }
    }
stage('Build') {
     steps {
            sh 'dotnet build --configuration Release'
      }
   }
stage('Pack') {
     steps {
           sh 'dotnet pack --no-build --output nupkgs'
      }
   }
stage('Publish') {
      steps {
           sh "dotnet nuget push **\\nupkgs\\*.nupkg -k yourApiKey -s http://myserver/artifactory/api/nuget/nuget-internal-stable/com/sample"
       }
   }
 }
}
