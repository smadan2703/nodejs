node {
    timestamps {
    def appPrefix = "Digital-Mortgage"
    def majorVersion = 1.0
    def currentVersion =""
    def commitId = ""
    def commitmessage = ""    
   // def branch = env.BRANCH_NAME
    def GIT_BRANCH = env.BRANCH_NAME
    def server = Artifactory.server 'jfrog'
    currentVersion = majorVersion+'.'+currentBuild.number
    def configTag = appPrefix+'-'+currentVersion

        stage ('code'){
            checkout scm        
            sh "git rev-parse HEAD > .git/commit-id"
            commitId = readFile('.git/commit-id') 
           // GIT_BRANCH = sh(returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
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
                    echo "${GIT_BRANCH}"
            } else if ("${GIT_BRANCH}" == 'UAT') {
                    echo "From UAT branch"
        }
            else { 
                echo "I am out"
            }
    }
        
    }
}









node {
   def pat = "/Users/devops/Desktop"
   def project = "Andriod"
   def version = "1.0.1"
   def con = "HLBKM"
   def envi = "PROD"
   def jf = "localj"
   def server = Artifactory.server "${jf}"
   def uploadSpec = """{
       "files" : [ {
           "pattern" : "${pat}/${project}-${version}.tar.gz",
           "target" : "HLBB/${con}/${project}/${envi}/${version}/"
       }
       ]
   }"""
   stage('Preparation') { // for display purposes
     
    server.upload(uploadSpec)
   }
  
}
