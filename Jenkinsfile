pipeline {
    agent {
        docker { image 'node:18.4.0-alpine' }
    }
    stages {
        stage ('Install'){
            steps{
                sh 'npm install'
                sh 'mkdir archive'
                zip zipFile: 'node_modules.zip', archive: false, dir: 'archive'
                archiveArtifacts artifacts: 'node_modules.zip', fingerpint: true
            }
        }

        stage('Test'){
            steps{
                copyArtifacts filter: 'node_modules.zip', fingerprintArtifacts: true, projectName: env.JOB_NAME, selector: specific(env.BUILD_NUMBER)
                unzip zipFile: 'node_modules.zip', dir: './node_modules'
                sh 'chmod u+x ./node_modules/.bin/*'
                sh 'npm test'
            }
        }
    }
}