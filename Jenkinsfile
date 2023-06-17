pipeline {
    agent any
    tools {
        maven 'maven'
        dockerTool 'docker'
    }
    stages{
       
        stage('BUILD'){
            steps{
                echo "BUILDING THE IMAGE... "
                
                sh "mvn clean package"
                sh "docker build -t intern/springapp:build-${BUILD_ID} ."
                
            }
        }
        
        stage('TAG'){
            steps{
                echo "TAGGING GIT REPO..."
                
                sh """
                git tag build-${BUILD_ID}
                git push origin --tags
                """

            }
        }
        stage('PUSH'){
            steps{
                echo "PUSHING THE IMAGE TO REPO ..."
                sh """
                docker tag intern/springapp:build-${BUILD_ID} ${USERNAME}/jenkins-maven:build-${BUILD_ID}
                docker push ${USERNAME}/jenkins-maven:build-${BUILD_ID}
                """
            }
        }
    }
    post {
        success {
            build job: 'Maven deploy', parameters: [string(name: 'BUILD', value: "$BUILD_ID")]
        }
    }
}
