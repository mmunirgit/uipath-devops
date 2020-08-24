pipeline {
    agent any 
    environment {
        MAJOR = '1'
        MANOR = '0'
    }
    stages {
        stage("build") {
            steps {
                checkout(
                    [$class: 'GitSCM',
                    branches: [[name: '*/master']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[credentialsId: env.GIT_CREDENTIALS_ID, url: env.GIT_URL]]]
                )
				
				UiPathPack (
				    outputPath: "${WORKSPACE}\\Output1\\jobs\\${JOB_NAME}\\builds\\${BUILD_NUMBER}\\", 
				    projectJsonPath: "${WORKSPACE}", 
				    version: CustomVersion('1.0.${BUILD_NUMBER}')
				)
				
				
            }    
                
        }
        
        stage("post-build") {
            steps {
                echo 'initializing post-build..'    
				
				UiPathDeploy (
					packagePath: "${WORKSPACE}\\Output1\\jobs\\${JOB_NAME}\\builds\\${BUILD_NUMBER}\\",
					orchestratorAddress: 'https:\\\\orch-1910.molab.com',
					orchestratorTenant: 'uipath',
					folderName: 'default',
					environments: 'dev',
					credentials: [$class: 'UserPassAuthenticationEntry', credentialsId: '43596ef1-00b1-4915-8b0b-ee219e2c363f']
				)
				
				cleanWs()
            }    
                
        }
        
        stage("deploy") {
            steps {
                echo 'deploying the application..'    
            }    
                
        }
    }

}
