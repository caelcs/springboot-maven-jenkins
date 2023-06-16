def scmvars
def image
node {    
    stage('clone') {
        // enabled by project type "Pipeline script from SCM"
        scmvars = checkout(scm)
        echo "git details: ${scmvars}"
    }
    stage('env') {
        // Jenkins provides no environment variable view
        sh 'printenv|sort'
    }
    stage('build') {
        // arg 1 is the image name and tag
        // arg 2 is docker build command line
        def customImage = docker.build("my-image:latest")
    }
    stage('push') {
        docker.withRegistry('http://192.170.200.2:5000') {
            image.push()
        }
    }
}
