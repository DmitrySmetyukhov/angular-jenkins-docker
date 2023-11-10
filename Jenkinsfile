pipeline {
  agent {
    docker { image 'node:latest' }
  }
  stages {
    stage('Install') {
      steps { sh 'npm install' }
    }
 
    stage('Test') {
      parallel {
        stage('Unit tests') {
            steps { 
              catchError(buildResult: 'FAILURE"){
                 sh 'npm run-script test' 
              }
            }
        }
      }
    }
 
    stage('Build') {
      steps { sh 'npm run-script build' }
    }
  }


   /* Cleanup workspace */
    post {
       always {
           deleteDir()
       }
    }
}
