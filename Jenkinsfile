pipeline {
    agent any
    tools {
        maven 'maven'
        dockerTool 'docker'
    }
    
    stages{
       
        stage('BUILD'){
            when {
                branch 'release/*'
            }
            steps{
                echo "Building... "
                
                sh "mvn clean package"
                sh "docker build -t intern/springapp ."
                
                echo "Tagging and pushing to ECR"
                echo "build-${BUILD_ID}"
                
//                 sh """
//                 git tag build-${BUILD_ID}
//                 git push origin --tags
//                 """
                
                // TODO : IMPLEMENT PUSH TO ECR
            }
        }
        
        stage('DEV_DEPLOY'){
            when {
                branch 'release/*'
            }
            steps{
                echo "Deploying docker container in dev env"
                // TODO : IMPLEMENT DEPLOYING CONTAINER
                script{
                       env.RELEASE = input message: 'Should we promote to QA ?', ok: 'Continue',
                             parameters: [booleanParam(name: 'QA_DEPLOY')] 
                }
                
            }
        }
        
        stage('QA_DEPLOY'){
             when {
                branch 'release/*' 
                 expression{
                     return env.RELEASE
                 }
            }
       
            steps{
                
                echo "Deploying docker container in QS"
                // TODO : APPROVAL STAGE TO PROMOTE TO QA
            }
        }
        
        stage('CLEANUP'){
             when {
                branch 'release/*'
            }
            steps{
                echo "Cleaning dangling containers and images"
                // TODO : IMPLEMENT CLEANUP
            }
        }
    }
}