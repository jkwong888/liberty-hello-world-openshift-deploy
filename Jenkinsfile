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
              sh "find ."

              files = findFiles(glob: '**/*.yaml')

              println "${files}"

              for (File f : files) {
                def objects = openshift.apply(readFile(f.path()))
                println "Created objects from path ${f.path()}:\n ${objects.names()}"
              }
            }
          }
        }
      }
    }
  }
}
