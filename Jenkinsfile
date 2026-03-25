pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/sumay2112/maven-web-app.git'
            }
        }

        stage('Compile the code') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test the code') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package the code') {
            steps {
                sh 'mvn package'
            }
        }

        stage('upload artifact to the nexus repository') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: 'http://your-nexus-url',          // replace with your Nexus URL
                    groupId: 'teksacademy.com',
                    version: '1.0-SNAPSHOT',
                    repository: 'maven-releases',              // your Nexus repo
                    credentialsId: 'your-nexus-credential-id', // Jenkins credential ID
                    artifacts: [
                        [artifactId: 'employee-form', type: 'war', file: 'target/employee-form-1.0-SNAPSHOT.war']
                    ]
                )
            }
        }
    }
}
