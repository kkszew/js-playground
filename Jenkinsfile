pipeline {
    agent {
        docker { image 'node:18.4.0-alpine' }
    }
    stages {
        stage ('Test'){
            steps{
                sh 'npm install'
                sh 'npm test'
            }
        }
    }
}