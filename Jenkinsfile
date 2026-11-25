pipeline {
    agent any

    options {
        timestamps()
        timeout(time: 15, unit: 'MINUTES')
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

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
            when {
                expression {
                    currentBuild.currentResult == 'SUCCESS'
                }
            }
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