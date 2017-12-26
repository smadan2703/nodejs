//# !/usr/bin/env groovy

node {
    timestamps {
    def appPrefix = "madan"
    def majorVersion = 1.0
    def currentVersion =""
    def commitId = ""
    def commitmessage = ""    
    def server = Artifactory.server 'jfrog'
    currentVersion = majorVersion+'.'+currentBuild.number
    def configTag = appPrefix+'-'+currentVersion
    
       stage('Prepare') {
          // echo "Project to Build: ${project}"
           echo "Project to Build: ${appPrefix}"
          // echo "Branch to Build: ${branch}"
           echo "Branch to Build: ${majorVersion}"
           // echo "Env to Deploy: ${env}"
           echo "ConfigTag: ${configTag}"
        }

        stage ('code'){
           //checkout scm
           checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/smadan2703/nodejs.git']]])
           sh "git rev-parse HEAD > .git/commit-id"
           commitId = readFile('.git/commit-id')
           commitmessage = readFile('.git/COMMIT_EDITMSG')
           sh 'whoami'
            echo "commitid: ${commitId}"
            echo "messa: ${commitmessage}"
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
