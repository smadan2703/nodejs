#!/usr/bin/env groovy

def appName = config.applicationName;
def majorVersion = 1.0
def currentVersion =""
def commitId = ""
def commitmessage = ""


node {
    timestamps {
    
    def server = Artifactory.server SERVER_ID
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
            sh 'rs run deploy -prod'
        }
        stage(Artifact){
             def server = Artifactory.server ""
            // Read the upload spec and upload files to Artifactory.
            def downloadSpec =
                    '''{
                    "files": [
                        {
                            "pattern": "libs-snapshot-local/*.zip",
                            "target": "dependencies/"
                        }
                    ]
                }'''
            def buildInfo1 = server.download spec: downloadSpec
            // Read the upload spec which was downloaded from github.
            def uploadSpec =
                    '''{
                    "files": [
                        {
                            "pattern": "resources/Kermit.*",
                            "target": "libs-snapshot-local"
                        }
                    ]
                }'''

            // Upload to Artifactory.
            def buildInfo2 = server.upload spec: uploadSpec
            // Merge the upload and download build-info objects.
            buildInfo1.append buildInfo2
            // Publish the build to Artifactory
            server.publishBuildInfo buildInfo1
        }
        stage(Publish){

        }
        stage(deploy){
        
        }
    }
}
