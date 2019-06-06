/**
* Jenkins Doc: https://jenkins.io/doc/
*
**/

pipeline {
  // run on master
  agent any

  stages {
    stage ("Deploy objects") {
      steps {
        script {
          openshift.withCluster() {
            openshift.withProject() {
              files = findFiles(glob: '**/*.yaml')

              for (File f : files) {
                def objects = openshift.apply( readFile(f.path) )
                println "Created objects from path ${f.path}:\n ${objects.names()}"
              }
            }
          }
        }
      }
    }
  }
}
