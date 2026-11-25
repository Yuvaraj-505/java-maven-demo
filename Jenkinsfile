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

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'SUCCESS: Application built successfully!'
        }

        failure {
            echo 'FAILURE: Application build failed!'
        }

        unstable {
            echo 'UNSTABLE: Check test results.'
        }

        changed {
            echo 'Build status changed!'
        }

        cleanup {
            echo 'Cleanup completed!'
        }
    }

}