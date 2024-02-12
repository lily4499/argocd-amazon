node {
    def app
    
    env.IMAGE = 'liliacr.azurecr.io/amazon_app'

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/lily4499/argocd-amazon.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'lily-git-credentials', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email konissil@gmail.com"
                        sh "git config user.name lily4499"
                        sh "cat deployment.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${IMAGE_TAG}+g' deployment.yml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-amazon.git HEAD:main"
             }
         }
     }
  }
}
