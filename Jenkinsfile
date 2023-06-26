node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
        app = docker.build("omkarpatel00/blue-test")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'github') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'Blue-Update-Deployment', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
