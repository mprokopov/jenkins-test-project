pipeline {
   agent { label 'api' }

   stages {
      stage('Hello') {
         steps {
                script {
                    echo sh(script: "env", returnStdout: true)
                    json = sh(script: "getVersion -source=gradle -build-id=${BUILD_ID}", returnStdout: true)
                    echo(json)
                    def version = readJSON text: json
                    echo(version.AssemblySemVer)
                    echo(version.SemVer)
                    echo(version.BranchName)
                }
         }
      }
   }
}
