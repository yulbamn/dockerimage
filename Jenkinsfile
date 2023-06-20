node {
    def app
    
    stage('Clone repository') {
        checkout scm
    }
    
    stage('Build image') {
       app = docker.build("zenaksacr.azurecr.io/shopping-web")
    }
    
    stage('Push image') {        
        docker.withRegistry('https://zenaksacr.azurecr.io', 'acr') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    }
}
