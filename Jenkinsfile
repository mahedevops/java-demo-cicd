node {

print "****  START: SET  VARIABLES  : START ****"
    def mavenHome   = "${tool 'MVN363'}/bin/mvn"
//    def branchName  = "${BRANCH_NAME}"
    def buildNum    = "${BUILD_NUMBER}"
    def serviceName = "demo-service"
    def imageName   = "demo-api"
	def dockerSwarm = "${SWARM_MANAGER_HOST}"
    def dockerRepo  = "${DOCKER_REPOSITORY}"


print "****  START: SCM  CHECKOUT  : START ****" 
    stage 'CHECKOUT'
    checkout scm
print "****  END: SCM  CHECKOUT  : END ****"


  stage 'BUILD APPLICATION'
      
      sh "${mavenHome} clean"
      sh "${mavenHome}  package"    
     
  stage 'BUILD DOCKER IMAGE'
      sh "docker build -t ${imageName}  ."

    stage 'TAG/PUSH IMAGE'

    sh "docker tag ${imageName} ${dockerRepo}/${imageName}"
	sh "docker login -u mahedevops -p Mahesh@143"
    sh "docker push ${dockerRepo}/${imageName}"

  //stage 'DEPLOY TO SWARM'

    //sh "chmod +x deploy.sh && ./deploy.sh ${dockerSwarm} ${dockerRepo}/${imageName} ${serviceName}"
       
}
