pipeline {
   agent 'api'

   stages {
      stage('Hello') {
         steps {
                script {
                    json = sh(script: "getVersion -source=node -build-id=${BUILD_ID}", returnStdout: true)
                    def version = readJSON text: json
                    echo(version)
                }
         }
      }
   }
}
