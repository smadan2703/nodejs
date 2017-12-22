//# !/usr/bin/env groovy

def appName = config.applicationName;
def majorVersion = 1.0
def currentVersion =""
def commitId = ""
def commitmessage = ""


node {
    timestamps {
    
    def server = Artifactory.server jfrog
    currentVersion = majorVersion+'.'+currentBuild.number
    def configTag = appPrefix+'-'+currentVersion
    
        stage(Prepare) {
            echo "Project to Build: ${project}"
            echo "Branch to Build: ${branch}"
            echo "Env to Deploy: ${env}"
        }

        stage (Checkout){
            checkout scm
            sh "git rev-parse HEAD > .git/commit-id"
            commitId = readFile('.git/commit-id')
            commitmessage = readFile('.git/COMMIT_EDITMSG')
        }
        stage(NodeJs) {
            sh 'npm install'
        }
        stage(Publish){
        }
        stage(deploy){
        
        }
    }
}
