pipeline {
    agent {
        docker { image 'node:20' }
    }
    stages {
        stage('Install') {
            steps {
                // installDependencies()
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run-script build'
            }
        }
    }

    /* Cleanup workspace */
    post {
        always {
            deleteDir()
        }
    }
}
