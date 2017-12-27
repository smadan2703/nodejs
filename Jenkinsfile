node {
    timestamps {
    def appPrefix = "Digital-Mortgage"
    def env = SIT
    def majorVersion = 1.0
    def currentVersion =""
    def commitId = ""
    def commitmessage = ""    
    def server = Artifactory.server 'jfrog'
    currentVersion = majorVersion+'.'+currentBuild.number
    def configTag = appPrefix+'-'+currentVersion

        stage ('code'){
           sh 'mkdir ${Digital-Mortgage}'  
           checkout([$class: 'GitSCM', branches: [[name: 'refs/heads//master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'git@github.com:heroku/node-js-sample.git']]])
           sh "git rev-parse HEAD > .git/commit-id"
        }

        stage('Prepare') {
           echo "Project to Build: ${appPrefix}"
           echo "Env to Deploy: ${env}"
           commitId = readFile('.git/commit-id')
           echo "commitid: ${commitId}"
        }

        stage('Build') {
           sh 'ng build --prod'
           sh ''
        }
        //stage(Publish){
        //}
        //stage(deploy){
        
        //}
    }
}
