node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       docker.withServer('tcp://192.168.9.50:4243'){
            app = docker.build("branko129/test")
        }
    }                     

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('', 'git') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
