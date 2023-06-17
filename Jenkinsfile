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
                echo "BUILDING THE IMAGE... "
                
                sh "mvn clean package"
                sh "docker build -t intern/springapp:build-${BUILD_ID} ."
                
            }
        }
    }
}
