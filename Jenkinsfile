pipeline {
   agent { label 'api' }

   stages {
      stage('Hello') {
         steps {
                script {
                    json = sh(script: "getVersion -source=git-tag -build-id=${BUILD_ID}", returnStdout: true)
                    echo(json)
                    def version = readJSON text: json
                    echo(version.AssemblySemVer)
                }
         }
      }
   }
}
