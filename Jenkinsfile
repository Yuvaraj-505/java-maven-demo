pipeline {

    agent any

    tools {
        maven 'Maven-3.9'
    }

    stages {

        stage('Build and Test') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'target/surefire-reports/*.xml'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }

    }

    post {
        success {
            echo 'Maven build successful!'
        }

        failure {
            echo 'Maven build failed!'
        }

        always {
            echo 'Pipeline completed.'
        }
    }
}