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
            echo 'Test report publishing attempted.'
        }

        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the test reports.'
        }
    }
}