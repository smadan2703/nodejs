node {
    timestamps {
    def appPrefix = "Digital-Mortgage"
    def envmadan = "SIT"
    def majorVersion = 1.0
    def artifacts = "/Users/devops/Jenkins/artifacts/"
    def currentVersion =""
    def commitId = ""
    def commitmessage = ""    
    def server = Artifactory.server 'jfrog'
    currentVersion = majorVersion+'.'+currentBuild.number
    def configTag = appPrefix+'-'+currentVersion

        stage ('code'){
                    //checkout([$class: 'GitSCM', branches: [[name: 'refs/heads/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/heroku/node-js-sample.git']]])
            checkout scm        
            sh "git rev-parse HEAD > .git/commit-id"
            commitId = readFile('.git/commit-id') 
        }

        stage('Prepare') { 
           
           echo "Project to Build: ${appPrefix}"
           echo "Env to Deploy: ${envmadan}"
           echo "commitid: ${commitId}"
        }

        stage('Build') {
            sh """ 
                npm install
                mkdir -p ${appPrefix}
                cp -rf public node_modules ${appPrefix}
                tar -zcf ${configTag}.tar.gz ${appPrefix}
            """
            sh 'ls -al'
        }
        stage('Artifact') {
        if (env.BRANCH_NAME == 'SIT') {
            sh """
                mv ${configTag}.tar.gz $artifacts
            """
        } else {
            echo "I will upload articats to Jfrog"
        }
    }
        // cp dist Server_Code/node_modules ${appPrefix}
        //stage('Artifact'){
         
        //}
        //stage(deploy){
        
        //}
    }
}
