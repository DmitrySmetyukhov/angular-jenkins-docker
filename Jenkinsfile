def installDependencies() {
    script {
        sh '''
            wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - &&
            echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list &&
            apt-get update &&
            apt-get install -y google-chrome-stable xvfb npm
        '''
    }
}

pipeline {
    agent {
        docker { image 'node:20' }
    }
    stages {
        stage('Install') {
            steps {
                installDependencies()
                sh 'npm install'
            }
        }

        stage('Test') {
            parallel {
                stage('Unit tests') {
                    steps {
                        catchError(buildResult: 'FAILURE') {
                            sh 'npm run-script test'
                        }
                    }
                }
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
