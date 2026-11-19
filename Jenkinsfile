pipeline {
    agent any

    tools {
        Updated upstream
        maven 'maven 3.9.9'
        maven 'maven-3.9.9'
        Stashed changes
    }

    options {
        timestamps()
        timeout(time: 30, unit: 'MINUTES')
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Maven application'
                sh 'mvn -B clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests'
                sh 'mvn -B test'
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving Maven artifacts'

                archiveArtifacts(
                    artifacts: 'target/*.jar,target/*.war',
                    fingerprint: true
                )
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed. Check Console Output.'
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}

