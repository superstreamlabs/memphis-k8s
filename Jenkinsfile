def gitBranch = "latest"
def gitURL = "git@github.com:Memphisdev/memphis-k8s.git"
def repoUrlPrefix = "memphisos"
import hudson.model.*
import groovy.transform.Field

node ("memphis-jenkins-big-fleet,") {
  git credentialsId: 'main-github', url: gitURL, branch: gitBranch
  
  try{

    stage('Login to Docker Hub') {
      withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_HUB_CREDS_USR', passwordVariable: 'DOCKER_HUB_CREDS_PSW')]) {
      sh 'docker login -u $DOCKER_HUB_CREDS_USR -p $DOCKER_HUB_CREDS_PSW'
      }
    }
    
    stage('Import version number from broker'){
      dir('memphis-broker'){
        git credentialsId: 'main-github', url: 'git@github.com:memphisdev/memphis.git', branch: gitBranch
      }
      sh """
        cat memphis-broker/version.conf | cut -d "-" -f1 > broker_version.conf
        rm -rf memphis-broker
      """
    }
   
    stage('Import version number from rest gateway'){
      dir('memphis-rest-gateway'){
        git credentialsId: 'main-github', url: 'git@github.com:memphisdev/memphis-rest-gateway.git', branch: gitBranch
      }
      sh "cat memphis-rest-gateway/version.conf > gw_version.conf"
      sh "rm -rf memphis-rest-gateway"
    }

 
    stage('Edit helm files') {
      sh """
        sed -i -r "s/version: [0-9].[0-9].[0-9]/version: \$(cat version.conf)/g" memphis/Chart.yaml
        sed -i -r "s/appVersion: \\"[0-9].[0-9].[0-9]/appVersion: \\"\$(cat broker_version.conf)/g" memphis/Chart.yaml
        sed -i -r "s/memphis-rest-gateway:[0-9].[0-9].[0-9]/memphis-rest-gateway:\$(cat gw_version.conf)/g" memphis/values.yaml
        sed -i -r "s/memphis:[0-9].[0-9].[0-9]/memphis:\$(cat broker_version.conf)/g" memphis/values.yaml
      """
      /* To Remove after release 1.1.3
      sh """
        sed -i -r "s/appVersion: [0-9].[0-9].[0-9]/appVersion: \$(cat version.conf)/g" memphis/index.yaml
        sed -i -r "s/version: [0-9].[0-9].[0-9]/version: \$(cat version.conf)/g" memphis/index.yaml
        sed -i -r "s/[0-9].[0-9].[0-9].tgz/\$(cat version.conf).tgz/g" memphis/index.yaml
      """
      */
      }

    stage('helm package'){
      sh"helm package memphis -d charts"
    }
    
    stage('helm create index'){
      dir ('charts'){
        sh"helm repo index ./ --url https://k8s.memphis.dev/charts/"
      }
    }

    stage('Install gh + jq') {
      sh """
        sudo dnf config-manager --add-repo https://cli.github.com/packages/rpm/gh-cli.repo -y
        sudo dnf install gh -y
        sudo dnf install jq -y
      """
    }
    stage('Push to latest'){
      withCredentials([sshUserPrivateKey(keyFileVariable:'check',credentialsId: 'main-github')]) {
        //sh "git reset --hard origin/master" //change to latest
        sh"""
          GIT_SSH_COMMAND='ssh -i $check'  git add charts/memphis-*
          GIT_SSH_COMMAND='ssh -i $check'  git commit -m "Version \$(cat version.conf)" -a
          GIT_SSH_COMMAND='ssh -i $check'  git push --set-upstream origin latest
        """
      }
      withCredentials([string(credentialsId: 'gh_token', variable: 'GH_TOKEN')]) {
        sh """
          gh release create v\$(cat version.conf) --generate-notes --target latest
        """
      }
    }
    
    stage('Checkout to version branch'){
      withCredentials([sshUserPrivateKey(keyFileVariable:'check',credentialsId: 'main-github')]) {
        sh"""
          GIT_SSH_COMMAND='ssh -i $check'  git checkout -b \$(cat version.conf)
          GIT_SSH_COMMAND='ssh -i $check'  git push --set-upstream origin \$(cat version.conf)
        """
      }
    }
    
    stage('Merge to gh-pages'){

    }

    notifySuccessful()
  
  }
    catch (e) {
      currentBuild.result = "FAILED"
      cleanWs()
      notifyFailed()
      throw e
  }
}
 def notifySuccessful() {
  emailext (
      subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':
        Check console output and connection attributes at ${env.BUILD_URL}""",
      recipientProviders: [requestor()]
    )
}
def notifyFailed() {
  emailext (
      subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':
        Check console output at ${env.BUILD_URL}""",
      recipientProviders: [requestor()]
    )
}  
