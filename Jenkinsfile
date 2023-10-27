pipeline {
  agent any
  stages {
    stage('update docker image') {
      steps {
        script {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            withCredentials([usernamePassword(credentialsId: 'git-hub-cred', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')])  {
              sh "git config user.email kimheangken68@gmail.com"
              sh "git config user.name KimheangKen"
              // sed : wanna change file 
              sh "sed -i \"s+kimheang68/jenkins-spring-build.*+kimheang68/jenkins-spring-build:${DOCKERTAG}+g\" dev/myapp-deployment.yaml"
              sh "git add ."
              sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
              sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argo-spring.git HEAD:master"
            }
          }
        }
      }
    }
  }
}