pipeline {
    agent any
    stages {
        stage('Update deployment') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
                        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]){
                        // withCredentials([usernamePassword(credentialsId: 'tuananh_github')]){
                            sh "git config user.email delta199502@gmail.com"
                            sh "git config user.name 'htrung'"
                            // sh "git config --unset http.proxy"
                            sh "cat deployment.yaml"
                            sh "sed -i 's+dckb9xz/todo.*+dckb9xz/todo:${DOCKERTAG}+g' deployment.yaml"
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done get update manifest version: ${env.BUILD_NUMBER}'"
                            // sh "echo ${GIT_PASSWORD}"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/deploy-argocd.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}
