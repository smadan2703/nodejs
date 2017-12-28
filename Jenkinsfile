node {
    timestamps {
    def appCountry = "HLBMY"   
    def appPrefix = "Digital-Mortgage"
    def majorVersion = 1.0
    def currentVersion =""
    def commitId = ""
    def commitmessage = ""    
    def gitBranch = env.BRANCH_NAME
    currentVersion = majorVersion+'.'+currentBuild.number
    def configTag = appPrefix+'-'+currentVersion

        stage ('code'){
            checkout scm        
            sh "git rev-parse HEAD > .git/commit-id"
            commitId = readFile('.git/commit-id') 
        }

        stage('Prepare') { 
           
           echo "Project to Build: ${appPrefix}"
           echo "Env to Deploy: ${gitBranch}"
           echo "commitid: ${commitId}"
        }

        stage('Build') {
            sh """ 
              ls
              #  npm install
              //  ng build --prod
              //  tar -zcf ${configTag}.tar.gz dist
            """
        }

        
        stage('Artifact') {
            if ("${gitBranch}" == 'SIT'|| "${gitBranch}" == 'master' || "${gitBranch}" == 'UAT') {
                    def server = Artifactory.server 'localj'
                    def uploadSpec = """{
                             "files" : [ {
                                            "pattern" : "${configTag}.tar.gz",
                                            "target" : "HLBB/${appCountry}/${appPrefix}/${gitBranch}/${majorVersion}/"
                                      } ]
                        }"""
                    
                    server.upload(uploadSpec)
                } 

            else { 
                echo "Artifact is not uploading to Jfrog"
            }
        }
        
    }
}
