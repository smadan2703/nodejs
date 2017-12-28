node {
    timestamps {
    def appPrefix = "Digital-Mortgage"
    def majorVersion = 1.0
    def currentVersion =""
    def commitId = ""
    def commitmessage = ""    
    def branch = env.BRANCH_NAME
    def server = Artifactory.server 'jfrog'
    currentVersion = majorVersion+'.'+currentBuild.number
    def configTag = appPrefix+'-'+currentVersion

        stage ('code'){
            checkout scm        
            sh "git rev-parse HEAD > .git/commit-id"
            commitId = readFile('.git/commit-id') 
        }

        stage('Prepare') { 
           
           echo "Project to Build: ${appPrefix}"
           echo "Env to Deploy: ${branch}"
           echo "commitid: ${commitId}"
        }

        stage('Build') {
            sh """ 
              //  npm install
              //  ng build --prod
              //  tar -zcf $configTag}.tar.gz dist
              ls -al
            """
        }

        stage('Artifact') {
             if (env.BRANCH_NAME == 'SIT'|| env.BRANCH_NAME == 'master' || env.BRANCH_NAME == 'UAT') {
                    echo "${branch}"
            } else {
            echo "I will upload articats to Jfrog"
        }
    }
        
    }
}
