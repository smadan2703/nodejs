node {
    timestamps {
    def appPrefix = "Digital-Mortgage"
    def envmadan = "SIT"
    def majorVersion = 1.0
    def artifacts = "/opt/artifacts/"
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
           echo "Env to Deploy: ${envmadan}"
           commitId = readFile('.git/commit-id')
           echo "commitid: ${commitId}"
           def barn = env.BRANCH_NAME
            echo "branch-name: ${barn}"
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
