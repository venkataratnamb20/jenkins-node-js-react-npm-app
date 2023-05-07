pipeline {
    agent {
        docker {
            image 'node:20-bullseye-slim' 
            args '-p 3000:3000' 
        }
    }
    options {
       buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '1', numToKeepStr: '10')
       quietPeriod 300
   }

    stages {
        stage('Build') { 
            steps {
		sh 'npm cache clear -f'
                sh 'npm install' 
            }
        }
	stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
	stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
