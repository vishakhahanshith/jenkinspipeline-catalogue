pipeline {
    agent { node { label 'AGENT-1' } }
    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Unit test') {
            steps {
                echo "unit testing is done here"
            }
        }
        // sonar-scanner command expects sonar-project.properties should be available 
        stage('Sonar Scan') {
            steps {
                sh "sonar-scanner"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deployment"
            }
        }
    }
}