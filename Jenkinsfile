node {
    timestamps {
    def appPrefix = "Digital-Mortgage"
    def env = "SIT"
    def majorVersion = 1.0
    def currentVersion =""
    def commitId = ""
    def commitmessage = ""    
    def server = Artifactory.server 'jfrog'
    currentVersion = majorVersion+'.'+currentBuild.number
    def configTag = appPrefix+'-'+currentVersion

        stage ('code'){
                    checkout([$class: 'GitSCM', branches: [[name: 'refs/heads/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/heroku/node-js-sample.git']]])
                    sh "git rev-parse HEAD > .git/commit-id"
        }

        stage('Prepare') { 
           echo "Project to Build: ${appPrefix}"
           echo "Env to Deploy: ${env}"
           commitId = readFile('.git/commit-id')
           echo "commitid: ${commitId}"
        }

        stage('Build') {
            sh """ 
                npm install
                mkdir -p ${appPrefix}
            """
        }
        //stage('Artifact'){
         //   dir ("$appPrefix") {
                    sh 'cp -rf ../node_modules .'
           //  } 
        //}
        //stage(deploy){
        
        //}
    }
}
