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
        // stage('Sonar Scan') {
        //     steps {
        //         sh "sonar-scanner"
        //     }
        // }
        stage('Build') {
            steps {
                sh 'ls -ltr'
                sh 'zip -r ./* --exclude=.git --exclude=.zip'
            }
        }
        stage('Publish Artifact') {
            steps {
                //sh 'ls -ltr'
                //sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: 'my.nexus.address',
                    groupId: 'com.roboshop',
                    version: '1.0.0',
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth', //This we have created in Jenkins
                    artifacts: [
                        [artifactId: catalogue,
                            classifier: '',
                            file: 'catalogue.zip', //my-service-' + version + '.jar'
                            type: 'zip']
        ]
     )
            }
        }
    }
    post{
        always{
            echo 'cleaning up workspace'
            deleteDir()
        }
    }
}