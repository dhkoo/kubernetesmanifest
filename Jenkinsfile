GITHUB_USER_EMAIL = "amainlog@gmail.com"
GITHUB_USER_NAME = "dhkoo"
IMAGE_PATH = "dhkoo93/test"

node {
  def app
  stage('Clone repository') {
    checkout scm
  }
  stage('Update GIT') {
    script {
      catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
          //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
          sh "git config user.email '${GITHUB_USER_EMAIL}'"
          sh "git config user.name '${GITHUB_USER_NAME}'"
          //sh "git switch master"
          sh "cat deployment.yaml"
          sh "sed -i 's+${IMAGE_PATH}.*+${IMAGE_PATH}:${DOCKERTAG}+g' deployment.yaml"
          sh "cat deployment.yaml"
          sh "git add ."
          sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
          sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:master"
        }
      }
    }
  }
}
