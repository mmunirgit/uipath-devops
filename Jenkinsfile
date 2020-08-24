pipeline {
    agent any 
    environment {
        MAJOR = '1'
        MANOR = '0'
    }
    stages {
        stage("build") {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: env.GIT_CREDENTIALS_ID, url: env.GIT_URL]]])
            }    
                
        }
        
        stage("test") {
            steps {
                echo 'testing the application..'    
            }    
                
        }
        
        stage("deploy") {
            steps {
                echo 'deploying the application..'    
            }    
                
        }
    }

}
