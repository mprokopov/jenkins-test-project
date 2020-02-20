pipeline {
   // agent { label 'api' }
    agent {
    kubernetes {
      label 'api'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  containers:
  - name: jnlp
    image: registry2.swarm.devfactory.com/visionmobile/jenkins-agent-api-build:1.0.5
    tty: true
  - name: version
    image: mprokopov/getversion:latest
    tty: true
"""
}
}

   stages {
      stage('Hello') {
         steps {
                container('version') {  
                script {
                        echo sh(script: "env", returnStdout: true)
                        json = sh(script: """
ln -s `pwd` /app && cd /app
getversion -source=git-tag -build-id=${BUILD_ID}
""", returnStdout: true)
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
}
