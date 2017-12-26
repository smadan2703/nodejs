//# !/usr/bin/env groovy

node {
    timestamps {
    def appPrefix = "DM"
    def majorVersion = 1.0
    def currentVersion =""
    def commitId = ""
    def commitmessage = ""    
    def server = Artifactory.server 'jfrog'
    currentVersion = majorVersion+'.'+currentBuild.number
    def configTag = appPrefix+'-'+currentVersion
    def dmgiturl =  "https://github.com/smadan2703/nodejs.git"
    
       stage('Prepare') {
          // echo "Project to Build: ${project}"
           echo "Project to Build: ${appPrefix}"
          // echo "Branch to Build: ${branch}"
           echo "Branch to Build: ${majorVersion}"
           // echo "Env to Deploy: ${env}"
           echo "ConfigTag: ${configTag}"
        }

        stage ('code'){
          // checkout scm
           checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: '$dmgiturl']]])
           sh "git rev-parse HEAD > .git/commit-id"
           commitId = readFile('.git/commit-id')
           //commitmessage = readFile('.git/COMMIT_EDITMSG')
           sh 'whoami'
           echo "commitid: ${commitId}"
           shortCommit = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
           echo "messa: ${shortCommit}"
        }
        stage('NodeJs') {
           sh 'npm install'
        }
        //stage(Publish){
        //}
        //stage(deploy){
        
        //}
    }
}
