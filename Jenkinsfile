pipeline {

    agent any

    tools {
        maven 'Maven-3.9'
    }

    stages {

        stage('Verify Maven') {
            steps {
                sh 'mvn -version'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
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