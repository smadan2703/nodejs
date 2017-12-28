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
            GIT_BRANCH = sh(returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
        }

        stage('Prepare') { 
           
           echo "Project to Build: ${appPrefix}"
           echo "Env to Deploy: ${GIT_BRANCH}"
           echo "commitid: ${commitId}"
        }

        stage('Build') {
            sh """ 
              ls
            """
        }
              //  npm install
              //  ng build --prod
              //  tar -zcf $configTag}.tar.gz dist
        
        stage('Artifact') {
            if ("${GIT_BRANCH}" == 'SIT'|| "${GIT_BRANCH}" == 'master' || "${GIT_BRANCH}" == 'UAT') {
                    echo "${branch}"
            } else if ("${GIT_BRANCH}" == 'HEAD') {
                    echo "From elseif branch"
        }
            else { 
                echo "I am out"
            }
    }
        
    }
}
