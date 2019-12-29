
def setupEnv() {
    ["PATH+MAVEN=${tool 'maven3'}/bin",
     "PATH+JAVA_HOME=${tool 'jdk1.8'}/bin"
     ]
}


def notifySlack(String buildStatus = 'STARTED') {
    
	
    buildStatus = buildStatus ?: 'SUCCESS'

    def color

    if (buildStatus == 'STARTED') {
        color = '#D4DADF'
    } else if (buildStatus == 'SUCCESS') {
        color = '#BDFFC3'
    } else if (buildStatus == 'UNSTABLE') {
        color = '#FFFE89'
    } else {
        color = '#FF9FA1'
    }

    def msg = "${buildStatus}: `${env.JOB_NAME}` #${env.BUILD_NUMBER}:\n More info at: ${env.BUILD_URL}"

    slackSend(color: color, channel: '#qa_test', message: msg)
}





node {

sauce('6acd7486-127e-4e13-ba9a-7cbe0764363a') {
    
	 try{
        notifySlack()
		
        timestamps {
                    
					
				stage('Compile & Testing') {
				
                withEnv(setupEnv()) {
				
                    checkout scm
                                       

                    try {
					
                        bat 'mvn test'
      
                    }
                    catch (Exception e) {
                        currentBuild.result = 'FAILURE'
						
						throw e
                    }
                }
            }
            
            
            
        }
    } finally {
        notifySlack(currentBuild.result)
       
    }
}

   
}
 
 

